# Module 4 – GLS, Synthesis-Simulation Mismatch and Blocking/Non-Blocking Statements

## 🎯 Objective

The objective of Module 4 was to understand Gate-Level Simulation (GLS), synthesis-simulation mismatch, and the difference between blocking and non-blocking assignments in Verilog.

The experiments covered:

- Gate-Level Simulation (GLS)
- GLS concepts and flow
- Synthesis-simulation mismatch
- Blocking and non-blocking statements
- Caveats with blocking statements
- GLS laboratory experiments
- Synthesis-simulation mismatch experiments
- Blocking statement mismatch experiments

---

## 📑 Contents

- [1. GLS Concepts and Flow](#1-gls-concepts-and-flow)
- [2. Synthesis-Simulation Mismatch](#2-synthesis-simulation-mismatch)
- [3. Blocking and Non-Blocking Statements](#3-blocking-and-non-blocking-statements)
- [4. Caveats with Blocking Statements](#4-caveats-with-blocking-statements)
- [5. GLS and Synthesis-Simulation Mismatch Lab](#5-gls-and-synthesis-simulation-mismatch-lab)
- [6. Blocking Statement Mismatch Lab](#6-blocking-statement-mismatch-lab)
- [7. Observations](#7-observations)
- [8. Conclusion](#8-conclusion)

---

# 1. GLS Concepts and Flow

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

---

# 2. Synthesis-Simulation Mismatch

A synthesis-simulation mismatch occurs when the behavior observed during RTL simulation differs from the behavior of the synthesized circuit.

Possible causes include:

- Incorrect RTL coding
- Improper use of blocking assignments
- Improper use of non-blocking assignments
- Incomplete sensitivity lists
- Incorrect combinational logic description
- Simulation-only behavior
- Differences in the interpretation of RTL during synthesis

---

# 3. Blocking and Non-Blocking Statements

Verilog provides two commonly used assignment types.

## 3.1 Blocking Assignment

Blocking assignments use the `=` operator.

Example:

```verilog
a = b;
```

The assignment is executed immediately, and the next statement waits until the assignment is completed.

Blocking assignments are generally used for combinational logic.

---

## 3.2 Non-Blocking Assignment

Non-blocking assignments use the `<=` operator.

Example:

```verilog
q <= d;
```

The assignment is scheduled and updated after the current simulation event.

Non-blocking assignments are generally used for sequential logic such as flip-flops.

---

# 4. Caveats with Blocking Statements

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

### Blocking Caveat – Synthesized Circuit

![Blocking Caveat Schematic](<images/blocking_ccaveat(schematic).png>)

---

# 5. GLS and Synthesis-Simulation Mismatch Lab

The laboratory experiments demonstrated the difference between RTL simulation and synthesized behavior.

## 5.1 Ternary Operator MUX – Schematic

The ternary operator was used to describe multiplexer functionality.

### Synthesized Circuit

![Ternary Operator MUX Schematic](<images/terenery_operator_mux(schematic)waveform.png>)

The synthesized result demonstrates the hardware implementation of the multiplexer described using the ternary operator.

---

## 5.2 Ternary Operator MUX – Testbench Waveform

The design was verified using a testbench and the resulting waveform was observed.

### GTKWave Result

![Ternary Operator MUX Waveform](<images/terenery_operator_mux(tb)waveform.png>)

The waveform verifies the functional behavior of the multiplexer for different input and select conditions.

---

## 5.3 Ternary Operator MUX – My Library

The design was also analyzed using the technology-specific library.

### Synthesized Circuit

![Ternary Operator MUX My Library Schematic](<images/terenery_operator_mux(schematic)waveform.png>)

### Testbench Waveform

![Ternary Operator MUX My Library Waveform](<images/terenery_operator_mux(tb)waveform(my_lib).png>)

The results demonstrate the effect of technology mapping on the synthesized implementation.

---

# 6. Blocking Statement Mismatch Lab

Blocking statements were studied to understand how coding style can create differences between simulation and synthesized hardware behavior.

## 6.1 Blocking Statement Caveat – Waveform

The blocking statement design was simulated and the resulting waveform was observed.

### GTKWave Result

![Blocking Caveat Waveform](<images/tb_blocking_caveat(waveform).png>)

The waveform demonstrates the behavior of the design when blocking assignments are used.

---

## 6.2 Blocking Statement Caveat – My Library

The same design was analyzed using the technology-specific library.

### GTKWave Result

![Blocking Caveat My Library Waveform](<images/tb_blocking_caveat(waveform)my_lib.png>)

The result helps demonstrate the relationship between RTL simulation, synthesis and technology mapping.

---

# 7. Observations

| Experiment | Observation |
|---|---|
| GLS | Gate-level simulation verifies the synthesized netlist |
| Synthesis-simulation mismatch | RTL and synthesized behavior can differ because of coding issues |
| Blocking assignment | Blocking assignments execute immediately |
| Non-blocking assignment | Non-blocking assignments model sequential updates |
| Blocking caveat | Incorrect use in sequential logic can cause unexpected behavior |
| Ternary operator MUX | The ternary operator can be synthesized into multiplexer logic |
| MUX waveform | Simulation verifies the functional behavior of the MUX |
| My library results | Technology mapping changes the gate-level implementation |
| Blocking waveform | Blocking assignments can produce different simulation behavior |
| Library waveform | Technology-mapped simulation helps verify the synthesized design |

---

# 8. Conclusion

Module 4 provided practical understanding of Gate-Level Simulation, synthesis-simulation mismatch, and blocking and non-blocking assignments in Verilog.

GLS was studied as an important verification step after synthesis. The experiments demonstrated how synthesized designs can be simulated and compared with RTL behavior.

The difference between blocking and non-blocking assignments was also studied. Blocking assignments are generally preferred for combinational logic, while non-blocking assignments are preferred for sequential logic.

The laboratory experiments demonstrated how the ternary operator can be synthesized into multiplexer logic and how incorrect use of blocking assignments can lead to unexpected simulation behavior.

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

The circuit diagrams and waveform screenshots included in this module were obtained from the Module 4 laboratory experiments.
