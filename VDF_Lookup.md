# VDF Lecture Content Lookup

Course: VLSI Design Flow (ECE313/ECE513) — Sneh Saurabh — Aug–Nov 2024.
Lookup of what each lecture PDF covers, derived from slide titles. Use to route questions to the correct file without re-scanning all PDFs.

Filename format in folder: `WeekXX_LY_Topic_YYYY-MM-DD.pdf`

## Module map (high level)
- **Weeks 1–4** Introduction (history, IC structure, fab flow, RTL→GDS overview, post-GDS, design styles, business model, FoMs, abstraction, behavioral synthesis)
- **Weeks 4–6** Logic Design (HDL/Verilog, simulation, RTL synthesis, synthesizable constructs, operators)
- **Weeks 6–7** Formal Verification (BDD/OBDD/ROBDD, SAT, model checking, CEC)
- **Weeks 7–10** Library + STA (Liberty, NLDM, setup/hold, timing graph, arrival/required/slack, slew prop, MMMC, OCV)
- **Weeks 10–11** DFT (fault models, scan design, ATPG, BIST)
- **Weeks 12–14** Physical Design (FEOL/BEOL, interconnect RC, signal integrity, floorplan/power/placement/CTS/routing/PV/signoff/ECO)

---

## Per-lecture index

### Week 1 – Introduction
**W1 L1 (12 Aug, 33pg)** Course admin (syllabus, evaluation, policies, Google Classroom). VLSI historical perspective. Structure of integrated circuit. Photolithography basics.
**W1 L2 (14 Aug, 28pg)** Fabrication (silicon wafer, dies, chips). Semiconductor business model (fabless / foundry / IDM). Different VLSI design flows. Types of ICs. Design styles: full-custom, standard-cell, gate-array, FPGA. Economics of ICs.

### Week 2 – Introduction (RTL → GDS overview)
**W2 L1 (19 Aug, 17pg)** Figures of Merit (FoMs). Chip designing inputs/outputs. RTL (Verilog, VHDL). Abstraction (concept, why, illustration). Pre-RTL methodologies. System-level design top view.
**W2 L2 (21 Aug, 18pg)** Hardware/software partitioning (motivation + example). RTL general structure. Functional specification → RTL. Behavioral synthesis (what + cost metrics).

### Week 3 – Introduction (Synthesis + PD overview)
**W3 L1 (28 Aug, 25pg)** Behavioral synthesis (illustration, trade-offs, untimed→timed, merits/challenges). Overview of RTL→GDS flow. Logic synthesis (inputs/outputs, illustration). IC terminology. Netlist attributes. Physical design intro + major tasks.
**W3 L2 (31 Aug, 18pg)** Physical design pipeline: chip planning, placement, CTS, routing (global + detailed), ECO + GDS writing, optimizations, iterative flow. Verification techniques: simulation, model checking, combinational equivalence.

### Week 4 – Introduction (Verification + Post-GDS) → Logic Design starts
**W4 L1 (2 Sep, 23pg)** Verification: STA, physical design verification. Manufacturing defects (origin, manifestation). Yield + clustering. Testing technique. ATE. Fault coverage + defect level. DFT. Post-GDS: mask fabrication, mask writing, RET, OPC, double/multiple patterning.
**W4 L2 (4 Sep, 21pg)** Wafer fab + die testing. Packaging. Final testing + binning. **Logic Synthesis recap.** HDL features. Verilog vs VHDL. Functional verification basics. Simulation framework. Testbench illustration. Code coverage.

### Week 5 – Logic Design (Simulation + RTL synthesis)
**W5 L1 (9 Sep, 17pg)** Code coverage vs functional coverage. Digital simulation. Event-driven vs cycle-based. Verilog simulation definitions. Event processing. Stratified queue mechanism. Race conditions in Verilog.
**W5 L2 (11 Sep, 21pg)** Logic synthesis mechanisms + tasks. RTL synthesis: parsing, elaboration, uniquification. Synthesizable vs non-synthesizable constructs. assign / if-else / case statements. Always blocks: edge-sensitive, blocking vs non-blocking, level-sensitive, unintentional latch inference, incomplete sensitivity list.

### Week 6 – Logic Design → Formal Verification (only L1; W6 L2 cancelled, public holiday)
**W6 L1 (18 Sep, 21pg)** For loops. Functions. Operators: synthesis tasks, resource sharing, speculation (resource unsharing), mapping + architecture selection. **Formal Verification intro:** limits of simulation, formal as alternative, differences from simulation, techniques. Boolean function representations (compactness, canonicity). BDD. Binary decision tree (variable order).

### Week 7 – Formal Verification
**W7 L1 (23 Sep, 21pg)** Binary decision tree variable order. OBDD (example, isomorphic). ROBDD. Satisfiability: problem definition, formulation, k-SAT. Formal verification usage. Model checking (framework, property specification, techniques).
**W7 L2 (25 Sep, 25pg)** Equivalence checking usage. Combinational Equivalence Checking (CEC): steps, register + port matching (illustration, techniques), miter creation, miter + equivalence, illustration, establishing equivalence, soundness. **Technology Libraries** intro: libraries in flow, Liberty format, timing arcs, CMOS timing — delay + slew definitions.

### Week 8 – STA (only L1; W8 L2 cancelled, Gandhi Jayanti)
**W8 L1 (30 Sep, 25pg)** Library: CMOS slew/delay characteristics, NLDM (Non-Linear Delay Model), advanced delay models. Setup/hold time definition + characteristics. Modeling setup/hold constraints. Other library info. **STA intro:** what STA does, synchronous circuit data propagation, synchronous behavior, zero clocking, double clocking, verification. Setup + hold requirements.

### Week 9 – STA (Constraints)
**W9 L1 (14 Oct, 17pg)** STA path types. Environment of design. Constraints: basics, application, origin, types. Clock constraints: sources, primary clock source definition, derived clock source definition. Clock signal attributes: latency, uncertainty.
**W9 L2 (16 Oct, 15pg)** Clock signal attribute: transition. Environment of design (recap). Input port constraints (set_input_delay), transition at input port. Output port constraints (set_output_delay), load at output port. Timing exceptions. Constant value to port/pin.

### Week 10 – STA (Timing computation + variations) → DFT begins
**W10 L1 (21 Oct, 21pg)** Timing graph. Delay calculation (stage, essential components). Arrival time computation (concept, method, maximum, complications). Required time computation (concept, method, setup analysis). Slack computation (illustration). Slew propagation: need, slew–delay relationship, bound on slew.
**W10 Bonus (22 Oct, 3pg)** Attendance vs Mid-Sem Marks correlation plots (ECE313 + ECE513). Not a content lecture.
**W10 L2 (23 Oct, 21pg)** Slew propagation: bound + max-case example. Variations: need to account, safety margins, MMMC (Multi-Mode Multi-Corner) analysis, OCV (On-Chip Variation) derate. **DFT intro:** designing for testability, structural testing, functional vs structural, fault models, stuck-at fault models.

### Week 11 – DFT
**W11 L1 (4 Nov, 19pg)** Stuck-at fault sites. Test vectors (definition, design for testability). Controllability + observability for combinational and sequential circuits. **Scan design flow:** modifications, modes, scan cells, scan chain formation (example), sequential→combinational, mechanism, tasks, cost, number of cycles required.
**W11 L2 (6 Nov, 22pg)** **ATPG:** objective, challenges, terminologies, controlling/non-controlling values, general approach, path sensitization, backtracking, redundant faults, redundant-fault-based optimization, challenges + solutions. **BIST:** distinguishing features, fault coverage vs random pattern, architecture, test pattern generator.

### Week 12 – Physical Design begins
**W12 L1 (11 Nov, 15pg)** BIST test response analyzer. Wrap-up of BIST. **IC fabrication:** FEOL processes, BEOL processes (intro).
**W12 L2 (13 Nov, 31pg)** Interconnects/wires nature. Wiring layers (direction, height). Interconnect resistance + capacitance (incl. capacitance of strip, multiple interconnects). **Signal integrity:** coupling effects, base delay, dynamic delay variation, glitches (what, how created, magnitude factors, when functional), antenna effect cause. PD inputs/outputs. Library Exchange Format (LEF).

### Week 13 – Physical Design (Floorplan + Placement)
**W13 L1 (18 Nov, 17pg)** Chip planning: implementation methodology, partitioning, budgeting, block implementation + top-level assembly. Hierarchical design merits/challenges. **Floorplanning:** basics, die size, IO cells (basics, package connection), large object (macro) placement, guidelines.
**W13 L2 (20 Nov, 20pg)** Macro placement guidelines (continued), standard cell rows. **Power planning:** components, PDN (Power Delivery Network), electromigration, voltage drop. **Placement:** basics, wirelength estimates, global placement techniques, legalization + detailed placement, timing-driven, congestion-driven, scan chain reordering.

### Week 14 – Physical Design (CTS, Routing, Signoff)
**W14 L1 (25 Nov, 22pg)** Spare cell placement. **CTS:** basics, terminologies, clock distribution network, symmetric tree architecture, mesh architecture, useful skews (concept + illustration + example + obtaining), post-CTS optimization. **Routing intro:** basics, global routing (goals, objectives, model).
**W14 L2 (27 Nov, 27pg)** Global routing (model continued, challenges). **Detailed routing:** goals, constraints, final optimization. Antenna effect. Reliability: via defects. Manufacturability. **Layout / circuit / parasitic extraction.** **Physical verification:** DRC, ERC, LVS. **Signoff** + ECO + tapeout.

---

## Quick topic → file index

| Topic | File(s) |
|---|---|
| Course syllabus / admin | W1 L1 |
| IC history, fab basics, photolithography | W1 L1, W1 L2 |
| Design styles, business model, economics | W1 L2 |
| FoMs, abstraction, RTL | W2 L1 |
| HW/SW partitioning, behavioral synthesis | W2 L2, W3 L1 |
| RTL → GDS overview | W3 L1, W3 L2 |
| Physical design pipeline overview | W3 L2 |
| Manufacturing defects, yield, ATE, post-GDS, RET/OPC | W4 L1 |
| Packaging, binning | W4 L2 |
| HDL features, simulation, testbench, coverage | W4 L2, W5 L1 |
| Verilog simulation mechanism, race conditions | W5 L1 |
| RTL synthesis (parsing, elaboration, uniquification) | W5 L2 |
| Synthesizable constructs, always blocks, latch inference | W5 L2 |
| For loops, functions, operators (sharing/speculation) | W6 L1 |
| BDD / OBDD / ROBDD | W6 L1, W7 L1 |
| SAT / k-SAT | W7 L1 |
| Model checking | W7 L1 |
| Equivalence checking / CEC / miter | W7 L2 |
| Liberty format, NLDM, timing arcs | W7 L2, W8 L1 |
| Setup/hold (definition, modeling) | W8 L1 |
| STA basics, zero/double clocking | W8 L1 |
| STA path types, constraints (input/output/clock) | W9 L1, W9 L2 |
| Clock latency, uncertainty, transition | W9 L1, W9 L2 |
| set_input_delay / set_output_delay / timing exceptions | W9 L2 |
| Timing graph, arrival/required/slack computation | W10 L1 |
| Slew propagation | W10 L1, W10 L2 |
| MMMC, OCV, variations, safety margins | W10 L2 |
| Fault models, stuck-at | W10 L2, W11 L1 |
| Controllability/observability | W11 L1 |
| Scan design, scan chain | W11 L1 |
| ATPG (path sensitization, backtracking, redundant) | W11 L2 |
| BIST (architecture, TPG, TRA) | W11 L2, W12 L1 |
| FEOL / BEOL fabrication | W12 L1 |
| Interconnect R, C, coupling | W12 L2 |
| Signal integrity, glitches, antenna effect | W12 L2 |
| LEF / PD inputs–outputs | W12 L2 |
| Chip planning, partitioning, hierarchical design | W13 L1 |
| Floorplanning, IO cells, macro placement | W13 L1, W13 L2 |
| Power planning, PDN, electromigration, IR drop | W13 L2 |
| Placement (global, legalization, timing-driven, congestion) | W13 L2 |
| Scan chain reordering | W13 L2 |
| CTS (skew, mesh, H-tree, useful skew) | W14 L1 |
| Global routing | W14 L1, W14 L2 |
| Detailed routing | W14 L2 |
| Antenna effect (PV side), via defects | W14 L2 |
| Layout / parasitic extraction | W14 L2 |
| DRC / ERC / LVS | W14 L2 |
| Signoff / ECO / tapeout | W14 L2 |
