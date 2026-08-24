# Module 5 – Optimization in Synthesis

## 🎯 Objective

The objective of Module 5 was to understand optimization in synthesis and how different Verilog RTL coding constructs affect the synthesized hardware.

The experiments covered:

- `if` and `case` constructs
- Incomplete `if` statements
- Incomplete `case` statements
- Incomplete overlapping case statements
- `for` loop
- `for generate`
- Ripple Carry Adder
- Multiplexer using generate
- Comparator using case
- Demultiplexer using case
- Demultiplexer using generate
- Synthesis and optimization using Yosys
- Simulation using Icarus Verilog
- Waveform analysis using GTKWave
- Technology mapping using the SKY130 standard-cell library

---

## 📑 Contents

- [1. If and Case Constructs](#1-if-and-case-constructs)
- [2. Labs on Incomplete If](#2-labs-on-incomplete-if)
- [3. Labs on Incomplete Overlapping Case](#3-labs-on-incomplete-overlapping-case)
- [4. For Loop and For Generate](#4-for-loop-and-for-generate)
- [5. Labs on For Loop and For Generate](#5-labs-on-for-loop-and-for-generate)
- [6. Observations](#6-observations)
- [7. Conclusion](#7-conclusion)

---

# 1. If and Case Constructs

The `if` and `case` constructs are used in Verilog to describe conditional and selection logic.

During synthesis, the RTL description is converted into hardware based on the conditions specified in the code.

Proper coding of conditional statements is important because incomplete or overlapping conditions can affect the synthesized hardware.

---

## 1.1 If Case Constructs – Part 1

The first experiment introduced the basic `if` and `case` constructs used for describing conditional logic.

---

## 1.2 If Case Constructs – Part 2

The second experiment examined different ways of describing conditional logic using `if` and `case` statements.

---

## 1.3 If Case Constructs – Part 3

The third experiment continued the study of `if` and `case` constructs and their effect during synthesis.

---

# 2. Labs on Incomplete If

An incomplete `if` statement occurs when an output is not assigned for all possible input conditions.

This type of RTL coding can result in unintended hardware during synthesis.

---

## 2.1 Incomplete If – Part 1

### Synthesized Circuit

![Incomplete If Schematic](<images/tb_incomp_if(schematic).png>)

### GTKWave Result

![Incomplete If Waveform](<images/tb_incomp_if(waveform).png>)

The schematic and waveform were used to analyze the behavior of the incomplete `if` implementation.

---

## 2.2 Incomplete If – Part 2

A second incomplete `if` experiment was performed to observe the resulting hardware and simulation behavior.

### Synthesized Circuit

![Incomplete If 2 Schematic](<images/tb_incomp_if2(schematic).png>)

### GTKWave Result

![Incomplete If 2 Waveform](<images/tb_incomp_if2(waveform).png>)

The waveform was analyzed for different input conditions to understand the behavior of the design.

---

# 3. Labs on Incomplete Overlapping Case

The `case` construct is commonly used to implement selection and decision logic.

An incomplete case statement does not specify an output for every possible condition. Overlapping conditions can also result in unexpected behavior.

---

## 3.1 Incomplete Case – Part 1

### Synthesized Circuit

![Incomplete Case Schematic](<images/tb_incomp_case(schematic).png>)

### GTKWave Result

![Incomplete Case Waveform](<images/tb_incomp_case(waveform).png>)

The experiment was used to study the behavior of incomplete case assignments during simulation and synthesis.

---

## 3.2 Incomplete Case – Part 2

Another incomplete case implementation was analyzed.

### GTKWave Result

![Bad Case Waveform](<images/tb_bad_case(waveform).png>)

The waveform demonstrates the behavior of the design for the tested input conditions.

---

## 3.3 Incomplete Case with Technology Library

The design was also analyzed using the technology-specific library.

### GTKWave Result

![Bad Case My Library Waveform](<images/tb_bad_case(waveform)(my_lib).png>)

The result demonstrates the behavior after technology-specific synthesis and mapping.

---

## 3.4 Partial Case Assignment

A partial case assignment was also studied.

### Synthesized Circuit

![Partial Case Assignment](<images/tb_partial_case_assign(schematic).png>)

The experiment demonstrates the importance of assigning outputs correctly in conditional combinational logic.

---

# 4. For Loop and For Generate

The `for` loop is used to describe repetitive operations in Verilog.

The `for generate` construct is used to create repeated hardware structures.

These constructs allow repetitive hardware to be described without writing the same RTL code multiple times.

---

## 4.1 For Loop and For Generate – Part 1

The first experiment introduced the use of `for` loops and `for generate` constructs.

---

## 4.2 For Loop and For Generate – Part 2

The second experiment examined how repetitive RTL structures are represented during synthesis.

---

## 4.3 For Loop and For Generate – Part 3

The third experiment continued the study of loop-based and generate-based hardware structures.

---

# 5. Labs on For Loop and For Generate

The following laboratory experiments were performed using `for` loops and `for generate` constructs.

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

The waveform demonstrates the routing of the input signal to the selected output.

---

## 5.5 Demultiplexer Using Generate

A generate-based demultiplexer was also implemented and simulated.

### GTKWave Result

![Demux Generate Waveform](<images/tb_demux_generate(waveform).png>)

The waveform was used to verify the operation of the generated demultiplexer.

---

# 6. Observations

| Experiment | Observation |
|---|---|
| If Case Constructs | Conditional RTL constructs were studied for describing selection logic |
| Incomplete If – Part 1 | Incomplete assignments were analyzed during synthesis and simulation |
| Incomplete If – Part 2 | A second incomplete `if` implementation was analyzed |
| Incomplete Case | Incomplete case behavior was studied |
| Bad Case | The effect of incomplete case coding was observed |
| My Library Case | Technology-specific library behavior was analyzed |
| Partial Case Assignment | Partial case assignment was studied |
| For Loop | Used to describe repetitive RTL operations |
| For Generate | Used to create repeated hardware structures |
| Ripple Carry Adder | Repetitive adder hardware was implemented and simulated |
| MUX Generate | Generate construct was used for multiplexer implementation |
| Comparator Case | Case construct was used for comparator implementation |
| Demux Case | Case construct was used for demultiplexer implementation |
| Demux Generate | Generate construct was used for demultiplexer implementation |

---

# 7. Conclusion

Module 5 provided practical understanding of optimization in synthesis and the effect of different Verilog coding constructs on hardware implementation.

The `if` and `case` experiments demonstrated how conditional RTL is interpreted during synthesis. Incomplete conditions and partial assignments were studied to understand their effect on the resulting hardware.

The module also introduced `for` loops and `for generate` constructs for describing repetitive hardware structures. Practical circuits including a Ripple Carry Adder, multiplexer, comparator and demultiplexer were implemented and verified.

Icarus Verilog was used for simulation, GTKWave was used for waveform analysis, and Yosys was used for synthesis and technology mapping.

The overall flow studied was:

```text
RTL Coding
     ↓
If / Case / For / Generate
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
