# ADDV Lecture Content Lookup

Course: Advanced Digital Design and Verification (ADDV) — Sneh Saurabh — Aug–Nov 2025.
Lookup of what each lecture PDF covers, derived from slide titles. Use to route questions to the correct file without re-scanning all PDFs.

Filename format in folder `Advanced-Degital-Design-&-Verification/lecture/`: `Week-XX_LY_Topic.pdf`

## Module map (high level)
- **Weeks 1** Introduction (course admin, electronic systems, HW/SW components, design + verification + manufacturing flow, software development process)
- **Weeks 1–2** ESL Design overview (motivation, flow, specification, partitioning, SW/HW implementation)
- **Weeks 2–4** SystemC (data types, modules, processes, events, signals, communication, channels, mutex, semaphore, fifo, sc_clock)
- **Weeks 3–4** Transaction-Level Modeling (TLM): basics, sockets, payload, blocking/non-blocking, quantum, temporal decoupling
- **Week 4** Virtual Platforms (definition, hybrid, examples, architectural exploration)
- **Week 5** HW/SW Partitioning + Platform-based Design + IP-XACT intro
- **Weeks 5–6** SoC Design Methodology (IP-XACT, IP Assembly) → High-Level Synthesis (CDFG, scheduling, binding, optimizations)
- **Weeks 7–11** SystemVerilog (data types, classes, inheritance, interface, clocking/program block, randomization, coverage, threads, IPC)
- **Weeks 11–12** SystemVerilog Assertions / SVA (immediate, deferred, concurrent, sequences, properties, LTL)
- **Weeks 12–13** UVM (architecture, phases, factory, virtual interface, class libraries, example) + PSS + SBSDT
- **Week 14** Clock Domain Crossing (CDC), Reset Domain Crossing (RDC), Power Analysis + Optimization, UPF intro

---

## Per-lecture index

### Week 1 – Introduction
**W1 L1 (12 Aug, 45pg)** Course admin (objectives, expected outcomes, pre-requisites, where to apply, course content table, Google Classroom, evaluation, assignments, exams, EDA server, references, policies on attendance/punctuality/plagiarism, office hours, expectations). Electronic system definition. Components of electronic systems. Hardware: processors (fixed-behavior, customizable, coprocessors, microcontrollers, ASIC). Memory. Software components. Mobile-phone example. System implementation bird's-eye view. Hardware design implementation (logic synthesis, physical design). Hardware design verification. Hardware manufacturing and test. Software development process. System integration and validation.
**W1 L2 (14 Aug, 30pg)** Electronic System Level (ESL) Design: motivation, definition, decisions/deliverables, flow, specification + ESL model (3 parts), pre-/post-partition analysis, partitioning, post-partitioning verification. Software implementation: waterfall vs spiral model, ESL applications, debuggability. Hardware implementation: co-processors, verification, verification IPs. **SystemC intro:** history, need, simulation environment, Hello World program, compiling.

### Week 2 – SystemC
**W2 L1 (19 Aug, 20pg)** SystemC Hello World recap. Compiling, shared object/library, running. Simulation phases (sc_main entry). SystemC overview (modules as basic blocks). **SystemC Data Types:** templates in C++, integers, fixed-point (basics + types), bitwise / arithmetic operations, sc_dt namespace, time definitions.
**W2 L2 (21 Aug, 22pg)** **Modules:** constructor role, module instances + design hierarchy. **SystemC Processes:** thread vs method, simulation kernel scheduling, syntax, initialize / evaluate-update phases, examples. **Events:** interactions between processes, immediate vs delayed notification (with example). **Sensitivity:** static vs dynamic, examples. **sc_signal:** evaluate-update paradigm, member functions.

### Week 3 – SystemC + TLM
**W3 L1 (26 Aug, 16pg)** Recap of immediate/delayed notification. **SystemC Communication:** abstract classes in C++, interfaces + channels + ports (4 parts), sc_port, sc_export, special ports sc_in/sc_out/sc_inout, instance connections, testbench, output (delta cycles).
**W3 L2 (28 Aug, 22pg)** **Channels:** primitive vs hierarchical, sc_mutex (with example), sc_semaphore (with example), sc_fifo<T>, sc_clock. **TLM Intro:** problem of HDL models, why TLM is faster, applications, basics (transactions), timing details (loosely-timed vs application). **SystemC TLM 2.0:** OSCI working group, sockets and payload, initiators and targets.

### Week 4 – TLM + Virtual Platforms
**W4 L1 (2 Sep, 22pg)** **TLM Transport:** blocking vs non-blocking mechanisms. Convenience sockets. **TLM Example (full):** setup, initiator, target, top, payload (memory-mapped bus + data), initiator thread, target response, result, summary (interoperability). **TLM More Concepts:** quantum, temporal decoupling, specialized transactions (debug, direct memory).
**W4 L2 (4 Sep, 26pg)** **Virtual Platforms:** definition, applications + benefits, hybrid VP, examples (vendors and tools). Architectural exploration illustration (Synopsys Platform Architect): problem, options, analysis, optimization, final result. **Partitioning intro:** basics, merits/demerits, key aspects, functional decomposition (2 parts), architecture description, components (CPUs, custom HW, standard HW, buses, OS).

### Week 5 – Partitioning + SoC Design Methodology
**W5 L1 (9 Sep, 23pg)** **Partitioning:** key aspects, approach (successive refinement), implementation considerations (HW + memory). **Platform-based Designs:** derivative designs, motivation, how to build (architectural + HW view), link between application and architecture, tasks + infrastructures (packaging IPs/interfaces, configuring parameters), challenges + improvements in IP assembly. **IP-XACT Intro:** introduction, salient features, XML basics, components, schema and parser.
**W5 L2 (11 Sep, 35pg)** **IP-XACT Elements:** component overview (2 parts). **Illustration (I2S protocol):** RTL views (3 parts), components, RTL view of structure (2 parts). **IP-XACT Details:** component, design, design configuration, summary. **IP Assembly:** SoC design methodology, open-source tools (verilog2ipxact, kactus2). **HLS Intro:** behavioral synthesis, transformations, RTL general structure, design decisions (FSM + hardware resources).

### Week 6 – High-Level Synthesis
**W6 L1 (16 Sep, 27pg)** **HLS Problem:** mapping IOs, three kinds of mapping (cycle-accurate, cycle-delayed, latency-insensitive). **HLS Flow:** typical flow, parsing, optimization (compiler examples: dead code elimination, etc.). **CDFG:** Control Flow Graph (basic blocks, definition, examples), Data Flow Graph, Single Static Assignment (SSA, phi function, optimization), combining CFG + DFG into CDFG.
**W6 L2 (18 Sep, 20pg)** **CDFG Optimizations.** **Initial Resource Allocation** (FU mapping). **Scheduling:** mapping operations to clock cycles, mapping hardware instances to operations. **Function Unit and Register Binding.** **Generate RTL** (FSM for control path). **HLS Optimizations:** loops (loop unrolling), arrays (3 ways + hazards), functions (inlining + as resource), pipelining (basics, throughput). **HLS Tools** (vendor list).

### Week 7 – SystemVerilog (only L1; L2 absent — Gandhi Jayanti 2 Oct)
**W7 L1 (30 Sep, 22pg)** Course content recap. **SystemVerilog Intro:** history, components. **Data Types:** overview, 4-state vs 2-state logic, static arrays (enhancements), packed/unpacked arrays, dynamic arrays, associative arrays (2 parts), queues, enum, struct/union, type conversion (static cast), packages. **Procedural Blocks intro.**

### Week 8 – SystemVerilog (Procedural Blocks + Classes)
**W8 L1 (7 Oct, 22pg)** Associative arrays corrections/clarification (2 parts). always_comb, always_latch behavior. **Procedural Block Enhancements (6 parts):** break/continue, function w/o return, default types, default arg values, pass-by-reference, etc. **SystemVerilog Classes:** encapsulation, role of new (constructor), customized constructor, object vs handle, garbage collection / object deallocation, access types (limiting variables), defining methods outside class (extern), static variables (2 parts).
**W8 L2 (9 Oct, 20pg)** **Classes (cont.):** scoping rules, containing object of other class, passing object to tasks/methods (2 parts), copying objects, shallow copy, customized copy, deep copy. **Inheritance:** basics, example, base class, extended class, constructor in extended class, virtual methods, casting (down/up), $cast.

### Week 9 – SystemVerilog (Inheritance + Interface + Clocking/Program Block)
**W9 L1 (14 Oct, 19pg)** **Inheritance (cont.):** parametrized classes, abstract classes + pure virtual methods. **Interface:** traditional connections without interface, interface introduction, connections (2 parts), modport. **Clocking Block:** declaration, usage, timing/clocking skew. **Program Block:** motivation (race conditions), example, timing regions intro.
**W9 L2 (16 Oct, 22pg)** Clarification slide. **Program Block (cont.):** SystemVerilog timing regions (2 parts). Clocking block + program block interplay. Sampling signal in testbench. Driving signal from testbench (synchronous). Program block example. Automatic vs static. **Coverage-driven Constrained-Random Testing (CRT):** directed vs CRT, effectiveness, randomization features (rand variables, constraints), coverage definitions (coverpoint, covergroup), coverage sampling, IMC output, increasing stimuli, adding constraints.

### Week 10 – SystemVerilog (Randomization) — only L1; L2 absent (Diwali / mid-sem break)
**W10 L1 (30 Oct, 22pg)** **Randomization:** cyclic random variables (rand vs randc), turning off randomness, randomization status, only checking constraints, **Constraints:** operators, bidirectional behavior, guiding probabilities, solve-before, implication, weighted distribution, inline constraints. Random number functions. pre_randomize / post_randomize. Randomizing arrays of data and arrays of handles. randcase. PRNG (pseudo-random number generator), seed impact, setting seed.

### Week 11 – SystemVerilog (Functional Coverage + Threads + IPC) → SVA
**W11 L1 (4 Nov, 32pg)** Clarification: weighted distribution (3 parts). **Functional Coverage:** metrics (bins, calculating coverage), automatic bins (2 parts), user-defined bins, conditional, transition, wildcard, ignoring values + illegal bins. **Cross Coverage:** basics, examples (2 parts), user-defined cover points, subset (2 parts). **Threads:** types, fork…join, fork…join_any, fork…join_none. **Inter-Process Communication (IPC):** event (2 parts), semaphore, mailboxes (2 parts).
**W11 L2 (6 Nov, 28pg)** Clarification: intersect (2 parts). Running coverage tools from Synopsys: VCS, simulate (simv), Verdi. **SystemVerilog Assertion (SVA) Intro:** introduction, example applications, simulation of good/bad design, formal property verification (FPV), assumption (definition + simulation + FPV), cover point (definition + simulation + FPV), assertion construct hierarchy (Boolean, sequence, assertion — 3 parts), types of assertions (immediate vs concurrent), immediate assertion (simulation + FPV examples).

### Week 12 – SystemVerilog Assertions
**W12 L1 (11 Nov, 31pg)** Recap (assertion types, timing regions). **Immediate Assertions:** evaluation, simple immediate assertion (simulation + formal), types (SIA + Deferred). **Deferred Immediate Assertions (DIA):** mechanism of reporting (2 parts), observed DIA (#0), final DIA. Assertion usage recommendation. **Concurrent Assertions:** basics, mechanism + evaluation, sampling example, sampled value functions, default clock and reset, sequences, delay operator (definition + examples), consecutive repetition operator (definition + examples), other operators (2 examples), goto repetition operator (definition + examples), cover property, implication operators (2 parts).
**W12 L2 (13 Nov, 15pg)** **Sequences (cont.):** non-consecutive repetition operator, goto repetition operator, combined examples. **Concurrent Assertions:** LTL operators, negated sequences, named sequences and properties, implicit multithreading, connecting properties with design (two ways). **UVM Intro:** basics, testbench (top-level entity), uvm_test class.

### Week 13 – UVM
**W13 L1 (18 Nov, 29pg)** **UVM Architecture:** environment (uvm_env), TLM in UVM, agent (uvm_agent), sequencer + driver + monitor (uvm_sequencer/driver/monitor), scoreboard (uvm_scoreboard). **UVM Phases:** standardized flow, major phases, phase example, order of phase execution in hierarchy, top-down build phase (3 parts), bottom-up connect phase (3 parts), run phase in parallel (3 parts). **UVM Factory:** basics, dynamic creation of object, command-line override. **Virtual Interface in UVM** (2 parts).
**W13 L2 (20 Nov, 27pg)** **UVM Class Libraries (3 parts):** building architecture, data classes, etc. **UVM Example (Full Walkthrough):** overview, NCSim file_list.f, DUT + interface + transaction (and_gate.sv), driver, monitor, environment, sequence, test, testbench top, output. **Portable Test and Stimulus Standard (PSS):** introduction, languages + model, usage + flow, developing model, portability, actions + activity, stimulus + coverage + checkers. **Scenario-based Software-driven Testing (SBSDT).**

### Week 14 – CDC + Power
**W14 L1 (25 Nov, 15pg)** **Clock Domain Crossing (CDC):** clock domains + crossings, forbidden event in flip-flop, consequences (Cases 1–4), problems associated with CDC, theory of synchronizers (metastability, probability of failure), double flip-flop synchronizer (2 parts), ensuring input data stability, data coherency challenges (multi-bit), CDC verification. **Reset Domain Crossing (RDC):** basics.
**W14 L2 (29 Nov, 20pg)** **Power Analysis:** components of power dissipation. **Dynamic Power:** switching power, short-circuit power. **Static Power.** Tech library models for dynamic + static power. Non-Linear Power Model (NLPM). Estimating power dissipation. **Power Optimization:** strategies, Dynamic Voltage Frequency Scaling (DVFS), Power Gating (basics + circuit elements), Clock Gating (basics + Integrated Clock Gater / ICG). **Power Intent:** Unified Power Format (UPF). Final-lecture closer ("Wishing you a bright future!").

### Standalone fragment
**Extra_CDC_ConsequencesOfForbiddenEvent.pdf (1pg)** Single page extracted from W14 L1 ("Consequences of Forbidden Event" — Cases 1–4 with pull-up/metastability summary). Likely an addendum or duplicate handout.

---

## Quick topic → file index

| Topic | File(s) |
|---|---|
| Course syllabus / admin / policies | W1 L1 |
| Electronic systems, HW/SW components | W1 L1 |
| HW design / verification / manufacturing flow | W1 L1 |
| Software development process, integration | W1 L1 |
| ESL motivation, flow, specification, partitioning | W1 L2 |
| Waterfall vs spiral software model | W1 L2 |
| HW implementation, co-processors, verification IPs | W1 L2 |
| SystemC history, need, Hello World | W1 L2, W2 L1 |
| SystemC data types (int, fixed-point, ops, time) | W2 L1 |
| SystemC modules, hierarchy, constructor | W2 L2 |
| SystemC processes (thread vs method, kernel) | W2 L2 |
| SystemC events, sensitivity (static/dynamic) | W2 L2, W3 L1 |
| sc_signal, evaluate-update paradigm | W2 L2 |
| Interfaces / channels / ports / sc_port / sc_export | W3 L1 |
| sc_in, sc_out, sc_inout, testbench | W3 L1 |
| sc_mutex, sc_semaphore, sc_fifo, sc_clock | W3 L2 |
| TLM basics, why faster, applications | W3 L2 |
| TLM 2.0 sockets, payload, initiators / targets | W3 L2 |
| TLM blocking / non-blocking transport | W4 L1 |
| TLM example (initiator/target/top/payload) | W4 L1 |
| TLM quantum, temporal decoupling, specialized | W4 L1 |
| Virtual platform definition + benefits + hybrid | W4 L2 |
| Architectural exploration (Synopsys Platform Architect) | W4 L2 |
| Partitioning basics, merits, decomposition | W4 L2, W5 L1 |
| Architecture components (CPUs, buses, OS) | W4 L2 |
| Platform-based design (derivative, build, link) | W5 L1 |
| IP-XACT intro, salient features, XML basics | W5 L1 |
| IP-XACT components, design, configuration | W5 L2 |
| IP-XACT illustration (I2S protocol) | W5 L2 |
| IP Assembly, verilog2ipxact, kactus2 | W5 L2 |
| HLS introduction, RTL structure, decisions, FSM | W5 L2 |
| HLS IO mapping (cycle-accurate, latency-insensitive) | W6 L1 |
| HLS flow: parsing, optimization, compiler opts | W6 L1 |
| CDFG: CFG, DFG, basic blocks, SSA, phi | W6 L1 |
| HLS scheduling, FU/register binding, RTL gen | W6 L2 |
| HLS optimizations (loops, arrays, functions, pipelining) | W6 L2 |
| HLS tools | W6 L2 |
| SystemVerilog history, components | W7 L1 |
| SV data types (4/2-state, arrays, queues, struct/union) | W7 L1 |
| SV packages, type conversion | W7 L1 |
| always_comb, always_latch, procedural enhancements | W8 L1 |
| SV classes (constructor, handle, deallocation, static) | W8 L1 |
| SV class scoping, copy (shallow/deep), passing | W8 L2 |
| SV inheritance, virtual methods, $cast | W8 L2 |
| Parametrized classes, abstract classes, pure virtual | W9 L1 |
| SV interface, modport | W9 L1 |
| Clocking block, program block, timing regions | W9 L1, W9 L2 |
| Sampling/driving signals in testbench | W9 L2 |
| Constrained-random testing (CRT), coverage basics | W9 L2 |
| Randomization (rand/randc, status, constraints) | W10 L1 |
| Constraints: operators, distribution, implication | W10 L1 |
| pre/post_randomize, randcase, PRNG, seed | W10 L1 |
| Functional coverage (bins, automatic, user-defined) | W11 L1 |
| Cross coverage | W11 L1 |
| SV threads, fork…join variants | W11 L1 |
| IPC: event, semaphore, mailbox | W11 L1 |
| Coverage tools (VCS, Verdi, IMC) | W9 L2, W11 L2 |
| SVA introduction, FPV, assumption, cover point | W11 L2 |
| Immediate assertions, deferred IA, simulation/FPV | W11 L2, W12 L1 |
| Concurrent assertions, sampling, default clock/reset | W12 L1 |
| Sequences, delay/repetition operators, cover property | W12 L1, W12 L2 |
| Implication operators | W12 L1 |
| LTL operators, named sequences/properties | W12 L2 |
| UVM basics, testbench, test class | W12 L2 |
| UVM architecture (env, agent, driver, monitor, scoreboard) | W13 L1 |
| UVM phases (build/connect/run, top-down/bottom-up) | W13 L1 |
| UVM factory, virtual interface | W13 L1 |
| UVM class libraries | W13 L2 |
| UVM full example (and_gate) | W13 L2 |
| PSS (Portable Test & Stimulus Standard) | W13 L2 |
| Scenario-based Software-driven Testing (SBSDT) | W13 L2 |
| Clock Domain Crossing (CDC), forbidden event, synchronizers | W14 L1 |
| Double flip-flop synchronizer, data coherency | W14 L1 |
| CDC verification, RDC | W14 L1 |
| Power dissipation: dynamic, static, NLPM | W14 L2 |
| Power optimization: DVFS, power gating, clock gating, ICG | W14 L2 |
| Unified Power Format (UPF), power intent | W14 L2 |

---

## Missing lectures (likely cancelled, not lost)
- **W7 L2** (~2 Oct 2025): coincides with **Gandhi Jayanti** national holiday.
- **W10 L2**: 14-day gap between W9 L2 (16 Oct) and W10 L1 (30 Oct) covers **Diwali (20 Oct) + mid-semester break**.
