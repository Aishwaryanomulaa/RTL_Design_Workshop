# Module 5 – Optimization in Synthesis

## 🎯 Objective

The objective of Module 5 was to understand optimization during RTL synthesis and to study how different Verilog coding constructs are interpreted by synthesis tools.

The experiments focused on `if`, `case`, `for` loop and `for generate` constructs. The effect of incomplete and overlapping conditions on synthesized hardware was also studied.

The experiments were performed using Icarus Verilog, GTKWave and Yosys with the SKY130 standard-cell library.

---

## 📑 Contents

- [1. If and Case Constructs](#1-if-and-case-constructs)
- [2. Incomplete If Case](#2-incomplete-if-case)
- [3. Incomplete Overlapping Case](#3-incomplete-overlapping-case)
- [4. For Loop and For Generate](#4-for-loop-and-for-generate)
- [5. Laboratory Experiments](#5-laboratory-experiments)
- [6. Observations](#6-observations)
- [7. Conclusion](#7-conclusion)

---

# 1. If and Case Constructs

The `if` and `case` constructs are commonly used in Verilog to describe conditional logic.

During synthesis, these constructs are converted into corresponding hardware depending on the conditions specified in the RTL.

Proper coding of conditional statements is important because incomplete or overlapping conditions can result in unintended hardware.

---

## 1.1 If Case Constructs – Part 1

The first experiment introduced the basic `if` and `case` constructs used to describe conditional logic.

---

## 1.2 If Case Constructs – Part 2

The second experiment examined different conditional coding structures and their interpretation during synthesis.

---

## 1.3 If Case Constructs – Part 3

The third experiment continued the study of `if` and `case` constructs and their effect on synthesized hardware.

---

# 2. Incomplete If Case

An incomplete `if` or `case` statement occurs when an output is not assigned for every possible input condition.

Such incomplete assignments can cause synthesis tools to infer unintended hardware.

---

## 2.1 Incomplete If – Part 1

The first incomplete `if` experiment was synthesized and simulated.

### Synthesized Circuit

![Incomplete If Schematic](<images/tb_incomp_if(schematic).png>)

### GTKWave Result

![Incomplete If Waveform](<images/tb_incomp_if(waveform).png>)

The schematic and waveform were used to study the behavior of the incomplete `if` implementation.

---

## 2.2 Incomplete If – Part 2

A second incomplete `if` experiment was performed to further analyze the synthesis and simulation behavior.

### Synthesized Circuit

![Incomplete If 2 Schematic](<images/tb_incomp_if2(schematic).png>)

### GTKWave Result

![Incomplete If 2 Waveform](<images/tb_incomp_if2(waveform).png>)

The waveform was analyzed for different input conditions.

---

# 3. Incomplete Overlapping Case

The `case` construct is useful for implementing selection and decision logic.

An incomplete case statement does not define an output for every possible condition. Overlapping case conditions can also result in unexpected behavior.

The experiments in this section focused on incomplete and overlapping case implementations.

---

## 3.1 Incomplete Case

### Synthesized Circuit

![Incomplete Case Schematic](<images/tb_incomp_case(schematic).png>)

### GTKWave Result

![Incomplete Case Waveform](<images/tb_incomp_case(waveform).png>)

The experiment was used to observe the behavior of an incomplete case implementation during simulation and synthesis.

---

## 3.2 Bad Case Implementation

A case implementation was analyzed to understand the effect of incomplete case conditions.

### GTKWave Result

![Bad Case Waveform](<images/tb_bad_case(waveform).png>)

The waveform shows the simulated behavior of the design for the tested input conditions.

---

## 3.3 Bad Case with Technology Library

The design was also analyzed using the technology-specific library.

### GTKWave Result

![Bad Case My Library Waveform](<images/tb_bad_case(waveform)(my_lib).png>)

The result demonstrates the behavior after technology-specific synthesis and mapping.

---

## 3.4 Partial Case Assignment

A partial case assignment was studied as part of the incomplete case experiments.

### Synthesized Circuit

![Partial Case Assignment Schematic](<images/tb_partial_case_assign(schematic).png>)

The experiment demonstrates the importance of properly assigning outputs in combinational RTL.

---

# 4. For Loop and For Generate

Verilog provides the `for` loop to describe repetitive operations.

The `for generate` construct can be used to create repeated hardware structures during elaboration.

These constructs allow repetitive hardware to be described without manually writing the same structure multiple times.

---

## 4.1 For Loop and For Generate – Part 1

The first experiment introduced the use of `for` loops and `for generate` constructs for describing repetitive hardware.

---

## 4.2 For Loop and For Generate – Part 2

The second experiment examined how repeated RTL structures are interpreted during synthesis.

---

## 4.3 For Loop and For Generate – Part 3

The third experiment continued the study of loop-based and generate-based hardware structures.

---

# 5. Laboratory Experiments

The following experiments demonstrated practical applications of the concepts studied in this module.

---

## 5.1 Ripple Carry Adder

A Ripple Carry Adder (RCA) was implemented using repetitive hardware structures.

### GTKWave Result

![RCA Waveform](<images/tb_rca(waveform).png>)

The waveform was analyzed to verify the sum and carry outputs for different input combinations.

---

## 5.2 Multiplexer Using Generate

A multiplexer was implemented using a generate construct.

### GTKWave Result

![MUX Generate Waveform](<images/tb_mux_generate(waveform).png>)

The waveform was used to verify the multiplexer operation for different input and select conditions.

---

## 5.3 Comparator Using Case

A comparator was implemented using a case-based RTL description.

### Synthesized Circuit

![Comparator Case Schematic](<images/tb_comp_case(schematic).png>)

### GTKWave Result

![Comparator Case Waveform](<images/tb_comp_case(waveform).png>)

The waveform was analyzed to verify the comparator output for different input combinations.

---

## 5.4 Demultiplexer Using Case

A demultiplexer was implemented using a case construct.

### GTKWave Result

![Demux Case Waveform](<images/tb_demux_case(waveform).png>)

The waveform demonstrates how the input signal is routed to the selected output.

---

## 5.5 Demultiplexer Using Generate

A generate-based demultiplexer was implemented and simulated.

### GTKWave Result

![Demux Generate Waveform](<images/tb_demux_generate(waveform).png>)

The waveform was used to verify the operation of the generated demultiplexer.

---

# 6. Observations

| Experiment | Observation |
|---|---|
| If Case Constructs | `if` and `case` constructs were studied for describing conditional logic |
| Incomplete If | Incomplete assignments were analyzed during synthesis and simulation |
| Incomplete If – Part 2 | A second incomplete `if` implementation was studied |
| Incomplete Case | The behavior of incomplete case conditions was analyzed |
| Bad Case | The effect of incomplete case coding was observed |
| Bad Case with My Library | Technology-specific synthesis and mapping were analyzed |
| Partial Case Assignment | Partial assignments in case logic were studied |
| For Loop | Used to describe repetitive RTL operations |
| For Generate | Used to create repeated hardware structures |
| Ripple Carry Adder | Repetitive adder hardware was implemented and simulated |
| MUX Generate | A generate construct was used for multiplexer implementation |
| Comparator Case | A case construct was used for comparator implementation |
| Demux Case | A case construct was used for demultiplexer implementation |
| Demux Generate | A generate construct was used for demultiplexer implementation |

---

# 7. Conclusion

Module 5 provided practical understanding of optimization in synthesis and the effect of different Verilog RTL coding constructs on hardware implementation.

The `if` and `case` experiments demonstrated how conditional statements are interpreted during synthesis. Incomplete assignments and overlapping conditions were studied to understand their effect on the resulting hardware.

The module also covered `for` loops and `for generate` constructs for describing repetitive hardware structures. Practical circuits including a Ripple Carry Adder, multiplexer, comparator and demultiplexer were implemented and verified.

Icarus Verilog was used for simulation, GTKWave was used for waveform analysis, and Yosys was used for synthesis and technology mapping.

The overall flow studied was:

```text
RTL Coding
     ↓
If / Case / For / Generate Constructs
     ↓
RTL Simulation
     ↓
Synthesis
     ↓
Optimization
     ↓
Technology Mapping
     ↓
Gate-Level Hardware
     ↓
Verification
```

The circuit diagrams and waveform screenshots included in this module were obtained from my own Module 5 laboratory experiments.
