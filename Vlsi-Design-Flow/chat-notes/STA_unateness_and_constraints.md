# STA — Unateness, Edge Direction, and Timing Constraints

Chat-derived notes. Covers things that often aren't spelled out in the slides: what STA actually tracks, how non-unate cells are handled, and why setup/hold are characterized per edge direction.

Related lecture material: W7 L2, W8 L1, W10 L1/L2 (see `VDF_Lookup.md`).

---

## 1. What STA tracks (and what it doesn't)

STA is **vectorless**. It does not simulate logic values or input patterns. It does not know whether a net is 1 or 0 at any time.

What it **does** track for every node:
- **Rise arrival time** and **fall arrival time** — separately.
- **Rise slew** and **fall slew** — separately.

Why per-direction? Because in CMOS, a 0→1 transition and a 1→0 transition are physically different events:
- Pull-up uses PMOS; pull-down uses NMOS.
- Hole mobility is ~2–3× lower than electron mobility → for equal W/L, PMOS is weaker than NMOS.
- Designers compensate by sizing PMOS wider, but the asymmetry never fully cancels out.

So delay (rise) ≠ delay (fall), and the .lib captures both.

**Net statement:** STA checks delay *as a function of edge direction*, but does not care which direction physically occurs in any given workload. It assumes the worst-case edge can happen on every path.

---

## 2. Unateness

Unateness = the **monotonic relationship** between an input edge direction and the output edge direction, *regardless of side-input state*.

| Category | Behavior | Examples |
|---|---|---|
| **Positive unate** | Input rise → output rise; input fall → output fall | AND, OR, buffer |
| **Negative unate** | Input rise → output fall; input fall → output rise | INV, NAND, NOR |
| **Non-unate (binate)** | Output direction depends on the state of other inputs | XOR, XNOR, MUX select pin |

### Common misconception: AOI and OAI are NOT non-unate
Any function built only from AND / OR / NOT (no XOR) is unate per input.
- AOI21 = !(A·B + C) is **negative unate** w.r.t. all three inputs.
- Pushing A higher → AND term up → OR term up → inverted output down. Always. Independent of B and C.
- The library just lists more arcs (one per input pin), not different kinds of arcs.

### The genuinely non-unate cells: XOR / XNOR / MUX-select
For XOR w.r.t. A:
- If B=0 → A rise causes Y rise (positive unate).
- If B=1 → A rise causes Y fall (negative unate).
- Behavior flips with side input → non-unate.

---

## 3. How the .lib encodes unateness

Each timing arc carries a `timing_sense` attribute:

```
timing_sense : positive_unate | negative_unate | non_unate
```

Number of delay tables per arc:
- **Positive unate** → 2 tables: rise→rise, fall→fall.
- **Negative unate** → 2 tables: rise→fall, fall→rise.
- **Non-unate** → **all 4 tables**: rise→rise, rise→fall, fall→rise, fall→fall. The vendor characterizes the cell under both side-input conditions and writes both sets of numbers.

---

## 4. How STA handles non-unate cells

At the output of an XOR/MUX, STA propagates **two candidate arrival times per output edge** — one assuming the arc was positive unate, one assuming negative unate.

Decision rule (universal in STA, not just non-unate):
- **Setup checks** → take **max** (worst case = slowest data, fastest clock).
- **Hold checks** → take **min** (worst case = fastest data, slowest clock).

Non-unate cells just contribute more candidate arrivals into the same max/min pool → more pessimism.

### Escape hatches that reduce pessimism
1. **`set_case_analysis`** — manually tell the tool a side input is constant (e.g. scan-enable tied low in functional mode). The XOR collapses to a buffer or inverter for the switching input; only relevant arcs are used.
2. **Constant propagation** — if the side input is hard-tied to VDD/VSS in the netlist, the tool figures it out automatically.

Without one of these, both senses are considered → worst case wins.

---

## 5. NLDM tables for setup and hold

Setup and hold are not single numbers per flop. They are **2D lookup tables** in the .lib (NLDM = Non-Linear Delay Model format), indexed by:
- **Constrained pin slew** — the data signal's transition time at D.
- **Related pin slew** — the clock signal's transition time at CK.

Skeleton:
```
pin (D) {
  timing() {
    related_pin : "CK";
    timing_type : hold_rising;
    rise_constraint (hold_template_7x7) {
      index_1 ("0.01, 0.05, 0.1, 0.3, 0.6, 1.0, 2.0");  // data slew
      index_2 ("0.01, 0.05, 0.1, 0.3, 0.6, 1.0, 2.0");  // clock slew
      values ( "0.012, 0.014, ...",
               "0.013, 0.015, ...",
               ... );
    }
    fall_constraint (...) { ... }
  }
  timing() {
    related_pin : "CK";
    timing_type : setup_rising;
    rise_constraint (...) { ... }
    fall_constraint (...) { ... }
  }
}
```

### Four constraint tables per flop per clock edge
- setup_rising — for rising D edge
- setup_falling — for falling D edge
- hold_rising — for rising D edge
- hold_falling — for falling D edge

### How the vendor builds these tables
SPICE **bisection**: for each (data_slew, clock_slew) grid point, sweep the data-to-clock arrival offset until the flop *just barely fails* (output flips wrong, or Q delay degrades by ~10%). That offset is the characterized setup or hold value at that grid point.

### How STA uses them
Look up actual data slew and clock slew at the flop → interpolate the table → plug into the setup/hold inequality. Same machinery as delay arcs, different table type.

---

## 6. Why setup/hold differ for rising vs falling D edge

Inside a flip-flop the master latch is a transmission gate feeding cross-coupled inverters with a keeper.
- **Rising D edge** → internal sampling node is pulled **up through PMOS**, fighting an NMOS keeper.
- **Falling D edge** → same node pulled **down through NMOS**, fighting a PMOS keeper.

Because PMOS and NMOS aren't symmetric (mobility difference), the minimum time D must be stable before CK to be reliably captured differs by edge direction. Usually tens of picoseconds, but real — and the .lib captures it.

### STA runtime behavior
- It knows the direction of the arriving D edge (because rise/fall arrivals are propagated separately).
- Picks `setup_rising`/`hold_rising` table for rising D arrivals, `setup_falling`/`hold_falling` for falling.
- Considers both possibilities and applies max (setup) / min (hold) pessimism.

Clock side has similar asymmetry — some libraries also distinguish rising vs falling clock-edge setup, relevant for negative-edge or dual-edge flops.

---

## 7. The single rule that ties it all together

> For every timing check on every path: **max for setup, min for hold.**

Non-unate cells, rise/fall direction splits, NLDM lookups — they all just feed candidates into this same pool. The pessimism stays consistent: assume the worst-case combination that can physically occur, because STA refuses to reason about whether it actually will.

---

## 8. Two mental models for timing — metastability vs STA

When reasoning about double clocking (or any setup/hold scenario), it helps to keep two distinct models in mind. STA enforces a *stricter* constraint than what physics alone demands, and the gap between the two is where most confusion lives.

### Model 1 — Metastability (physics)

This is the model an electrical engineer uses when staring at a flip-flop's internal transistors.

- **Rule:** the D pin must not transition during the aperture `[T − Tsetup, T + Thold]` around the capture clock edge.
- **What happens otherwise:** if D transitions inside the aperture, the master latch's internal node lands in a metastable state — Q is undefined and may take an unbounded time to resolve.
- **What is permitted:** D may transition *anywhere outside* the aperture, including arbitrarily early. If a D transition lands well before `T − Tsetup`, the new value is already stable when the edge fires, and the flop deterministically samples the new value with no metastability.

This model only flags electrical failure (metastability). It does **not** flag wrong-data capture.

### Model 2 — STA (abstraction)

This is the model an STA tool uses to certify a chip in polynomial time without simulation.

- **Rule:** every D transition must land in the narrow *stable band* between the previous edge's hold-close and the next edge's setup-open: `(T_prev + Thold, T_next − Tsetup)`.
- **What it forbids in addition to Model 1:** transitions that arrive *too early* (before `T + Thold` of the launching edge) — these would be sampled cleanly as wrong-cycle data, no metastability, but the chip computes garbage.
- **Why the harder cap:** STA's job is to guarantee the RTL semantics that synthesis promised — each register samples exactly the intended value each cycle. "Electrically clean but logically wrong" is still a chip-killing bug, so STA forbids it statically.

### The three regions, side by side

For a path with positive skew (capture clock later than launch), let `t_arrival = T1 + Tcq + Tcombo` be when new data reaches FF2's D pin:

| Region | t_arrival relative to FF2 aperture `[T2 − Tsu, T2 + Th]` | Physics says | STA says |
|---|---|---|---|
| **A** | Before the aperture (`t_arrival < T2 − Tsu`) | Safe — new data cleanly captured | **Violation** — wrong data on this edge (double clocking) |
| **B** | Inside the aperture | **Violation** — metastability | **Violation** — metastability |
| **C** | After the aperture (`t_arrival > T2 + Th`) | Safe — old data cleanly captured | Safe — old data cleanly captured (correct) |

STA's hold constraint `Tcombo ≥ Skew + Thold − Tcq` pushes you into Region C. The metastability-only boundary `Tcombo ≥ Skew − Tsetup − Tcq` would only push you out of Region B and into Region A — electrically fine, functionally broken.

### Why the STA abstraction is worth it

The harder cap isn't pessimism for pessimism's sake. It buys three things:

1. **Computational tractability.** With the cap, each node carries scalar (arrival, slew) values per edge direction. No logical state, no simulation. Max/min algebra closes the analysis in polynomial time.
2. **RTL-semantic correctness.** Synthesis promised the netlist implements the RTL. STA's cap is precisely the constraint that makes that promise hold. Without it, you could deliver a chip that doesn't glitch but computes the wrong function.
3. **Vectorless guarantee.** Because the cap is logic-value-independent, STA doesn't need to know what data is on any wire to sign off the design.

### Other physics-for-tractability trades STA makes

The metastability-vs-STA gap is the most pedagogically obvious abstraction, but it's not the only one. The full stack:

- Waveform shape → reduced to (arrival, slew).
- Cell electrical state → ignored, only edge direction matters (hence rise/fall arcs and unateness).
- PVT → discretized to a handful of corners (MMMC).
- On-chip variation → lumped into derate factors (OCV / AOCV / POCV).
- Crosstalk → separate SI pass bumps delays and slews, then STA re-runs.
- Switching-activity-dependent IR drop → folded into a worst-case voltage assumed at each cell.

Each trade loses some accuracy and gains the ability to bound timing across the entire input space without simulation. STA is the whole stack of such trades, not just the double-clocking cap.

### Where Model 1 still matters

The metastability-only view doesn't go away just because STA exists. It's the right tool whenever you intentionally allow Region A or Region B behavior:

- **Asynchronous boundaries / synchronizers** — metastability is allowed and resolved over multiple cycles. STA's hard cap doesn't apply across the async boundary; the metastability model + MTBF math takes over.
- **Latch-based / time-borrowed pipelines** — transparent latches widen the sampling aperture in a controlled way. The data-arrival vs metastability-aperture distinction is what makes time borrowing safe.
- **Min-delay padding (hold fixing)** — when inserting buffers to fix a hold violation, knowing whether you're in Region A (just functional) vs Region B (metastable) changes how much padding you need and where.
