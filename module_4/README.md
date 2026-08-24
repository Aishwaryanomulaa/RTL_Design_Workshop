# Module 4 – GLS, Synthesis-Simulation Mismatch and Blocking/Non-Blocking Statements

## 🎯 Objective

The objective of Module 4 was to understand Gate-Level Simulation (GLS), synthesis-simulation mismatch, and the difference between blocking and non-blocking assignments in Verilog.

The experiments covered:

- Gate-Level Simulation (GLS)
- GLS concepts and flow using Icarus Verilog
- Synthesis-simulation mismatch
- Blocking statements in Verilog
- Non-blocking statements in Verilog
- Caveats associated with blocking statements
- Laboratory experiments on GLS
- Laboratory experiments on synthesis-simulation mismatch
- Synthesis-simulation mismatch caused by blocking statements

---

## 📑 Contents

- [1. GLS, Synthesis-Simulation Mismatch and Blocking/Non-Blocking Statements](#1-gls-synthesis-simulation-mismatch-and-blockingnon-blocking-statements)
- [2. Labs on GLS and Synthesis-Simulation Mismatch](#2-labs-on-gls-and-synthesis-simulation-mismatch)
- [3. Labs on Synthesis-Simulation Mismatch for Blocking Statements](#3-labs-on-synthesis-simulation-mismatch-for-blocking-statements)
- [4. Key Concepts](#4-key-concepts)
- [5. Observations](#5-observations)
- [6. Conclusion](#6-conclusion)

---

# 1. GLS, Synthesis-Simulation Mismatch and Blocking/Non-Blocking Statements

## 1.1 GLS Concepts and Flow Using Icarus Verilog

Gate-Level Simulation (GLS) is the process of simulating the synthesized gate-level netlist to verify that the synthesized design behaves as expected.

The basic GLS flow is:

```text
RTL Design
    ↓
RTL Simulation
    ↓
Synthesis
    ↓
Gate-Level Netlist
    ↓
Gate-Level Simulation
    ↓
Verification
```

GLS helps verify the functionality of the synthesized design and can reveal issues that may not be visible during RTL simulation.

### GLS Concepts and Flow

![GLS Concepts and Flow](images/SKY130RTL_D4SK1_L1_GLSConceptsAndFlowUsingIverilog.svg)

---

## 1.2 Synthesis-Simulation Mismatch

A synthesis-simulation mismatch occurs when the behavior observed during RTL simulation differs from the behavior of the synthesized circuit.

Such mismatches can occur because of:

- Incorrect RTL coding
- Improper use of blocking assignments
- Improper use of non-blocking assignments
- Incomplete sensitivity lists
- Incorrect combinational logic description
- Simulation-only behavior
- Differences between RTL and synthesized hardware interpretation

### Synthesis-Simulation Mismatch

![Synthesis-Simulation Mismatch](images/SKY130RTL_D4SK1_L2_SynthesisSimulationMismatch.svg)

The purpose of studying synthesis-simulation mismatch is to understand how RTL coding styles can affect the final hardware implementation.

---

## 1.3 Blocking and Non-Blocking Statements in Verilog

Verilog provides two commonly used assignment types:

### Blocking Assignment

Blocking assignments use the `=` operator.

Example:

```verilog
a = b;
```

The assignment is executed immediately, and the next statement waits until the assignment is completed.

Blocking assignments are generally used for combinational logic.

### Non-Blocking Assignment

Non-blocking assignments use the `<=` operator.

Example:

```verilog
q <= d;
```

The assignment is scheduled and updated after the current simulation event.

Non-blocking assignments are generally used for sequential logic such as flip-flops.

### Blocking vs Non-Blocking

![Blocking and Non-Blocking Statements](images/SKY130RTL_D4SK1_L3_BlockingAndNonBlockingStatementsInVerilog.svg)

---

## 1.4 Caveats with Blocking Statements

Blocking assignments can cause unexpected behavior when they are used incorrectly in sequential logic.

For example:

```verilog
always @(posedge clk)
begin
    q1 = d;
    q2 = q1;
end
```

Because blocking assignments execute immediately, `q2` can receive the updated value of `q1` during simulation.

Using non-blocking assignments:

```verilog
always @(posedge clk)
begin
    q1 <= d;
    q2 <= q1;
end
```

causes both assignments to use the values from before the clock event, which more accurately represents flip-flop behavior.

### Caveats with Blocking Statements

![Caveats with Blocking Statements](images/SKY130RTL_D4SK1_L4_CaveatsWithBlockingStatements.svg)

---

# 2. Labs on GLS and Synthesis-Simulation Mismatch

The laboratory experiments demonstrated the difference between RTL simulation and gate-level simulation.

The synthesized netlist was simulated to verify the behavior of the design after synthesis.

---

## 2.1 GLS and Synthesis-Simulation Mismatch – Part 1

The first laboratory experiment demonstrated GLS and the behavior of the synthesized design.

### Lab Result

![GLS Synth Sim Mismatch Part 1](images/SKY130RTL_D4SK2_L1_Lab_GLS_Synth_Sim_Mismatch_part1.svg)

The experiment helped in understanding how the synthesized netlist can be simulated and compared with the original RTL behavior.

---

## 2.2 GLS and Synthesis-Simulation Mismatch – Part 2

The second laboratory experiment continued the analysis of GLS and synthesis-simulation mismatch.

### Lab Result

![GLS Synth Sim Mismatch Part 2](images/SKY130RTL_D4SK2_L2_Lab_GLS_Synth_Sim_Mismatch_part2.svg)

The comparison between RTL simulation and gate-level simulation helps identify possible differences introduced during synthesis.

---

# 3. Labs on Synthesis-Simulation Mismatch for Blocking Statements

Blocking assignments were studied to understand how coding style can create differences between simulation and synthesized hardware behavior.

---

## 3.1 Blocking Statement Mismatch – Part 1

The first experiment demonstrated synthesis-simulation mismatch caused by the use of blocking statements.

### Lab Result

![Blocking Statement Mismatch Part 1](images/SKY130RTL_D4SK3_L1_Lab_Synth_sim_mismatch_blocking_statement_part1.svg)

The experiment shows why blocking assignments must be used carefully when describing sequential circuits.

---

## 3.2 Blocking Statement Mismatch – Part 2

The second experiment further demonstrated the effect of blocking statements on synthesis and simulation.

### Lab Result

![Blocking Statement Mismatch Part 2](images/SKY130RTL_D4SK3_L2_Lab_Synth_sim_mismatch_blocking_statement_part2.svg)

The experiment helps illustrate how incorrect assignment styles can result in different simulation and synthesized behavior.

---

# 4. Key Concepts

## Gate-Level Simulation

GLS verifies the synthesized gate-level netlist by simulating it using a testbench.

```text
RTL
 ↓
Synthesis
 ↓
Gate-Level Netlist
 ↓
Simulation
 ↓
Verification
```

---

## Synthesis-Simulation Mismatch

A synthesis-simulation mismatch occurs when the synthesized circuit does not behave in the same way as expected from RTL simulation.

Common causes include:

- Incorrect coding style
- Blocking assignments in sequential logic
- Incomplete sensitivity lists
- Incomplete combinational descriptions
- Incorrect reset handling
- RTL constructs that synthesis interprets differently

---

## Blocking Assignment

```verilog
=
```

Blocking assignments execute immediately.

They are generally preferred for:

```text
Combinational Logic
```

Example:

```verilog
always @(*) begin
    y = a & b;
end
```

---

## Non-Blocking Assignment

```verilog
<=
```

Non-blocking assignments update signals after the current simulation event.

They are generally preferred for:

```text
Sequential Logic
```

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

---

# 5. Observations

| Experiment | Observation |
|---|---|
| GLS concepts | Gate-level simulation verifies the synthesized netlist |
| Synthesis-simulation mismatch | RTL and synthesized behavior can differ because of coding issues |
| Blocking assignment | Blocking assignments execute immediately |
| Non-blocking assignment | Non-blocking assignments model sequential updates |
| Blocking statement caveats | Incorrect use in sequential logic can cause unexpected simulation behavior |
| GLS Lab Part 1 | Demonstrated gate-level simulation and mismatch analysis |
| GLS Lab Part 2 | Further comparison of RTL and synthesized behavior |
| Blocking mismatch Part 1 | Demonstrated mismatch caused by blocking statements |
| Blocking mismatch Part 2 | Further demonstrated the effect of blocking assignments |

---

# 6. Conclusion

Module 4 provided practical understanding of Gate-Level Simulation, synthesis-simulation mismatch, and Verilog assignment statements.

GLS was studied as an important verification step after synthesis. The experiments demonstrated how a synthesized gate-level netlist can be simulated and compared with the original RTL behavior.

The difference between blocking and non-blocking assignments was also studied. Blocking assignments are generally suitable for combinational logic, while non-blocking assignments are preferred for sequential logic.

The laboratory experiments demonstrated that incorrect RTL coding practices, especially the inappropriate use of blocking assignments in sequential logic, can result in synthesis-simulation mismatches.

The overall flow studied was:

```text
RTL Design
    ↓
RTL Simulation
    ↓
Synthesis
    ↓
Gate-Level Netlist
    ↓
Gate-Level Simulation
    ↓
Comparison
    ↓
Verification
```

The diagrams and laboratory results included in this module were obtained from the Module 4 experiments.
