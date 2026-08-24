# Module 5 – Optimization in Synthesis

## 🎯 Objective

The objective of Module 5 was to understand how RTL coding styles affect synthesis and the resulting hardware implementation.

The module focused on `if`, `case`, `for` loop and `for generate` constructs. The experiments also demonstrated how incomplete assignments, overlapping conditions and different RTL descriptions can affect simulation and synthesis.

The designs were simulated using Icarus Verilog, waveforms were analyzed using GTKWave, and synthesis and technology mapping were performed using Yosys and the SKY130 standard-cell library.

---

## 📑 Contents

- [1. RTL Coding Styles: IF-ELSE and CASE Statements](#1-rtl-coding-styles-if-else-and-case-statements)
- [2. Incomplete IF and CASE Constructs](#2-incomplete-if-and-case-constructs)
- [3. Incomplete and Overlapping CASE](#3-incomplete-and-overlapping-case)
- [4. FOR Loop and FOR Generate](#4-for-loop-and-for-generate)
- [5. Laboratory Experiments](#5-laboratory-experiments)
- [6. Observations](#6-observations)
- [7. Conclusion](#7-conclusion)

---

# 1. RTL Coding Styles: IF-ELSE and CASE Statements

RTL coding describes the behavior of a digital circuit before it is converted into gates during synthesis.

The way RTL is written determines how the synthesis tool interprets the intended hardware. Conditional statements are commonly used to select data, control operations and describe decision-making logic.

---

## 1.1 Priority Logic Using IF-ELSE

An `if-else` structure evaluates conditions in a defined order.

If multiple conditions are true, the first true condition takes priority.

Example:

```verilog
always @(*) begin
    if (condition_1)
        y = value_1;
    else if (condition_2)
        y = value_2;
    else
        y = value_3;
end
```

The priority can be understood as:

| Statement | Priority |
|---|---|
| `if` | Highest |
| `else if` | Next |
| `else` | Lowest |

Therefore, `if-else` is useful when the order in which conditions are evaluated is important, such as in priority encoders and control logic.

---

## 1.2 Selection Logic Using CASE

A `case` statement compares a selector expression with a set of possible values.

Example:

```verilog
always @(*) begin
    case (sel)
        2'b00: y = a;
        2'b01: y = b;
        2'b10: y = c;
        default: y = d;
    endcase
end
```

This coding style is useful when different input values select different operations or data paths.

Common applications include:

- Multiplexers
- Decoders
- State machines
- Control logic

---

## 1.3 IF-ELSE and CASE Comparison

| Feature | IF-ELSE | CASE |
|---|---|---|
| Main purpose | Priority-based decisions | Multi-way selection |
| Evaluation | Conditions are checked sequentially | Selector is compared with case items |
| Typical applications | Priority logic and control | MUX, decoder and FSM |
| Main coding concern | Condition ordering and completeness | Coverage and overlapping patterns |

The choice between `if-else` and `case` depends on the intended hardware behavior and the relationship between the conditions.

---

# 2. Incomplete IF and CASE Constructs

An incomplete conditional statement occurs when an output is not assigned for every possible input condition.

For combinational logic, outputs should normally be assigned for all required conditions. Otherwise, synthesis may infer storage behavior.

---

## 2.1 Incomplete IF

An incomplete `if` statement does not provide an assignment when the condition is false.

Example:

```verilog
always @(*) begin
    if (sel)
        y = a;
end
```

When `sel` is false, `y` is not assigned a new value.

This can result in latch inference during synthesis because the circuit needs to retain the previous value of the output.

### Synthesized Circuit

![Incomplete IF Schematic](<images/tb_incomp_if(schematic).png>)

The synthesized schematic represents the hardware inferred from the incomplete `if` RTL description.

### Simulation and Waveform Analysis

![Incomplete IF Waveform](<images/tb_incomp_if(waveform).png>)

The waveform shows the relationship between the input condition and the output during simulation.

When the condition does not result in a new assignment, the output can retain its previous value. This demonstrates why completeness is important when writing combinational RTL.

---

## 2.2 Incomplete IF – Second Experiment

A second incomplete `if` implementation was studied to observe its behavior during simulation and synthesis.

### Synthesized Circuit

![Incomplete IF 2 Schematic](<images/tb_incomp_if2(schematic).png>)

The schematic shows the synthesized hardware corresponding to the RTL implementation.

### Simulation and Waveform Analysis

![Incomplete IF 2 Waveform](<images/tb_incomp_if2(waveform).png>)

The waveform was analyzed to observe the output response for the different input conditions applied by the testbench.

The experiment demonstrates how incomplete conditional assignments can affect the behavior of combinational RTL.

---

# 3. Incomplete and Overlapping CASE

The `case` construct is commonly used to describe multi-way selection logic.

A case statement can become problematic when not all required conditions are covered or when multiple conditions can overlap.

Incomplete and overlapping case conditions can produce unintended behavior and may affect the hardware inferred during synthesis.

---

## 3.1 Incomplete CASE

An incomplete case statement does not specify an output for every possible selector value.

Example:

```verilog
always @(*) begin
    case (sel)
        2'b00: y = a;
        2'b01: y = b;
    endcase
end
```

Here, the cases for `2'b10` and `2'b11` are not specified.

A `default` assignment or complete case coverage can be used when appropriate to ensure that the output is defined.

### Synthesized Circuit

![Incomplete CASE Schematic](<images/tb_incomp_case(schematic).png>)

The schematic shows the hardware produced from the incomplete case RTL.

### Simulation and Waveform Analysis

![Incomplete CASE Waveform](<images/tb_incomp_case(waveform).png>)

The waveform shows the output behavior for the selector values tested by the testbench.

This experiment demonstrates the importance of complete assignments when describing combinational logic.

---

## 3.2 Bad CASE Implementation

A case implementation was analyzed to study the effect of incomplete or improperly specified case conditions.

### Simulation and Waveform Analysis

![Bad CASE Waveform](<images/tb_bad_case(waveform).png>)

The waveform shows the simulated response of the design for the input combinations applied during the experiment.

The result demonstrates how the RTL coding of conditional statements can influence the observed output behavior.

---

## 3.3 CASE Implementation with Technology Library

The design was also analyzed using the technology-specific library.

### Simulation Result

![Bad CASE My Library](<images/tb_bad_case(waveform)(my_lib).png>)

The result shows the behavior after the design was processed using the technology-specific library.

Technology mapping allows the RTL description to be represented using cells available in the selected standard-cell library.

---

## 3.4 Partial CASE Assignment

A partial case assignment was also studied.

### Synthesized Circuit

![Partial CASE Assignment](<images/tb_partial_case_assign(schematic).png>)

The synthesized schematic shows the hardware resulting from the partial case assignment.

This experiment demonstrates why outputs should be assigned appropriately for the required input conditions when designing combinational logic.

---

# 4. FOR Loop and FOR Generate

Verilog provides the `for` loop to describe repetitive operations.

The `for generate` construct is used to create repeated hardware structures.

These constructs are especially useful when the same hardware structure needs to be repeated multiple times.

---

## 4.1 FOR Loop

A `for` loop can be used inside procedural blocks to perform repetitive operations.

Example:

```verilog
for (i = 0; i < 4; i = i + 1)
begin
    ...
end
```

During synthesis, the loop is elaborated into the corresponding hardware structure.

The loop therefore provides a convenient way of describing repeated operations without writing the same RTL statements multiple times.

---

## 4.2 FOR Generate

A `for generate` construct can be used to create multiple instances of a hardware structure.

Example:

```verilog
genvar i;

generate
    for (i = 0; i < 4; i = i + 1)
    begin
        ...
    end
endgenerate
```

Generate constructs are evaluated during elaboration and are useful for creating repeated hardware structures such as adders, multiplexers and other regular circuits.

---

## 4.3 FOR Loop and FOR Generate Comparison

| Feature | FOR Loop | FOR Generate |
|---|---|---|
| Purpose | Repetitive procedural operations | Repeated hardware generation |
| Used during | Procedural execution / synthesis interpretation | Elaboration |
| Common use | Repeated assignments and calculations | Multiple hardware instances |
| Benefit | Reduces repetitive RTL code | Creates regular hardware structures |

---

# 5. Laboratory Experiments

The following experiments demonstrate practical applications of the concepts studied in this module.

---

## 5.1 Ripple Carry Adder

A Ripple Carry Adder (RCA) was implemented using repetitive full-adder structures.

The carry output of one stage is connected to the carry input of the next stage.

### Simulation and Waveform Analysis

![RCA Waveform](<images/tb_rca(waveform).png>)

The waveform shows the applied input combinations along with the resulting sum and carry outputs.

The simulation verifies the functional operation of the Ripple Carry Adder for the tested input conditions.

---

## 5.2 Multiplexer Using FOR Generate

A multiplexer was implemented using a generate-based hardware structure.

### Simulation and Waveform Analysis

![MUX Generate Waveform](<images/tb_mux_generate(waveform).png>)

The waveform shows the input, select and output signals during simulation.

The output changes according to the selected input, demonstrating the operation of the generated multiplexer structure.

---

## 5.3 Comparator Using CASE

A comparator was implemented using a `case` construct to describe the required comparison logic.

### Synthesized Circuit

![Comparator CASE Schematic](<images/tb_comp_case(schematic).png>)

The schematic represents the synthesized comparator logic.

### Simulation and Waveform Analysis

![Comparator CASE Waveform](<images/tb_comp_case(waveform).png>)

The waveform shows the input combinations and the corresponding comparator output.

The simulation was used to verify the comparison behavior of the RTL design.

---

## 5.4 Demultiplexer Using CASE

A demultiplexer was implemented using a `case` construct.

A demultiplexer routes a single input to one of several outputs depending on the select signal.

### Simulation and Waveform Analysis

![Demux CASE Waveform](<images/tb_demux_case(waveform).png>)

The waveform shows how the selected output responds to the input signal while the select lines determine the active output path.

This verifies the functional behavior of the case-based demultiplexer.

---

## 5.5 Demultiplexer Using FOR Generate

A generate-based demultiplexer was also implemented.

The repeated output-selection structure can be described efficiently using a generate construct.

### Simulation and Waveform Analysis

![Demux Generate Waveform](<images/tb_demux_generate(waveform).png>)

The waveform shows the output response for the different select conditions.

The simulation verifies that the input is routed to the appropriate output according to the select signal.

---

# 6. Observations

| Experiment | Observation |
|---|---|
| IF-ELSE | Conditions are evaluated in priority order |
| CASE | Selector values are compared with specified case items |
| Incomplete IF | Missing assignments can result in latch inference |
| Incomplete IF – Second Experiment | The effect of incomplete conditional assignment was observed |
| Incomplete CASE | Missing case conditions can leave the output incompletely specified |
| Bad CASE | Improper case coding can affect the simulated and synthesized behavior |
| CASE with Technology Library | Technology-specific mapping was observed |
| Partial CASE Assignment | Output completeness is important for combinational logic |
| FOR Loop | Useful for describing repetitive RTL operations |
| FOR Generate | Useful for creating repeated hardware structures |
| Ripple Carry Adder | Repeated full-adder structures were used to implement addition |
| MUX Generate | Generate construct was used to create a multiplexer structure |
| Comparator CASE | CASE construct was used to implement comparison logic |
| Demux CASE | CASE construct was used to implement output selection |
| Demux Generate | Generate construct was used to create repeated demultiplexer logic |

---

# 7. Conclusion

Module 5 provided practical understanding of RTL coding constructs and their effect on synthesis.

The `if-else` and `case` constructs were studied as methods for describing priority and selection logic. Incomplete assignments were examined to understand how missing conditions can affect the behavior and hardware inferred during synthesis.

The module also introduced incomplete and overlapping case conditions and demonstrated the importance of complete and unambiguous RTL coding.

The `for` loop and `for generate` constructs were studied for describing repetitive hardware structures. Practical circuits including a Ripple Carry Adder, multiplexer, comparator and demultiplexer were implemented and verified.

Icarus Verilog was used for simulation, GTKWave was used for waveform analysis, and Yosys was used for synthesis and technology mapping.

The overall flow studied was:

```text
RTL Coding
     ↓
IF / CASE / FOR / GENERATE
     ↓
RTL Simulation
     ↓
Waveform Analysis
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
