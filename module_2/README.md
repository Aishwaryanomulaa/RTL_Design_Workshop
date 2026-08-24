# Module 2 – Timing Libraries, Hierarchical vs Flat Synthesis & Flip-Flop RTL Coding Styles

## 🎯 Experiment Objective

The objective of Module 2 was to understand **technology timing libraries, hierarchical and flattened synthesis, and different flip-flop RTL coding styles**.

The experiments focused on studying the SKY130 `.lib` file, understanding how synthesis uses technology-library information, comparing hierarchical and flattened synthesis, and implementing different types of flip-flops using Verilog RTL.

The designs were simulated using **Icarus Verilog**, waveform results were analyzed using **GTKWave**, and synthesis and technology mapping were performed using **Yosys**.

---

## 📑 Contents

- [1. Technology Libraries](#1-technology-libraries)
- [2. Hierarchical and Flattened Synthesis](#2-hierarchical-and-flattened-synthesis)
- [3. Flip-Flop RTL Coding Styles](#3-flip-flop-rtl-coding-styles)
- [4. Simulation and Synthesis](#4-simulation-and-synthesis)
- [5. Observations](#5-observations)
- [6. Conclusion](#6-conclusion)

---

# 1. Technology Libraries

A technology library contains information about the standard cells that can be used during synthesis.

It provides information such as:

- Cell functionality
- Timing characteristics
- Power information
- Operating conditions
- Cell area

The SKY130 library used in this experiment was:

```text
sky130_fd_sc_hd__tt_025C_1v80.lib
```

The filename represents the operating conditions of the library:

| Part | Meaning |
|---|---|
| `tt` | Typical process |
| `025C` | Temperature of 25°C |
| `1v80` | Supply voltage of 1.8 V |

The `.lib` file can be opened and examined using:

```bash
gedit sky130_fd_sc_hd__tt_025C_1v80.lib
```

This allows the available standard cells and their timing information to be inspected.

### 📷 SKY130 `.lib` File

![SKY130 Library](https://github.com/user-attachments/assets/7bf75f62-4888-4244-90fb-07d948804610)

The library file contains descriptions of the available cells and their characteristics. This information is used by synthesis tools when converting RTL into technology-specific hardware.

---

# 2. Hierarchical and Flattened Synthesis

Synthesis can either preserve the structure of an RTL design or combine the modules into a single-level representation.

---

## 2.1 Hierarchical Synthesis

In hierarchical synthesis, the relationships between different RTL modules are maintained.

A simple representation is:

```text
        Top Module
        /        \
   Module A    Module B
```

This approach preserves the organization of the original RTL design and makes individual modules easier to identify.

### 📷 Hierarchical Synthesis

![Hierarchical Synthesis](https://github.com/user-attachments/assets/46b3f459-8efa-4149-8ac2-36d6915c6fe4)

The synthesized representation shows that the module hierarchy is maintained rather than combining all logic into one flat structure.

---

## 2.2 Flattened Synthesis

Flattening removes the module boundaries and combines the design into a single-level representation.

```text
Module A ──┐
           ├──► Flat Design
Module B ──┘
```

Flattening gives the synthesis tool greater freedom to optimize logic across module boundaries.

### 📷 Flattened Synthesis

![Flattened Synthesis](https://github.com/user-attachments/assets/83b31d8b-c046-4b55-8d50-74a3b9e85dab)

The synthesized representation shows the modules combined into a single-level design.

---

## 2.3 Hierarchical vs Flattened Synthesis

| Feature | Hierarchical | Flattened |
|---|---|---|
| Module hierarchy | Preserved | Removed |
| Optimization | More localized | Across the design |
| Debugging | Easier | More difficult |
| Structure | Modular | Unified |

The choice between hierarchical and flattened synthesis depends on the requirements of the design and the desired optimization and implementation flow.

---

# 3. Flip-Flop RTL Coding Styles

Flip-flops are sequential elements used to store data.

Their output is controlled by a clock and may also include reset or set signals.

Different RTL coding styles can describe different types of flip-flop behavior.

---

## 3.1 Asynchronous Reset D Flip-Flop

An asynchronous reset can change the flip-flop output without waiting for a clock edge.

Example:

```verilog
module dff_asyncres (
    input clk,
    input async_reset,
    input d,
    output reg q
);

always @(posedge clk, posedge async_reset)
begin
    if (async_reset)
        q <= 1'b0;
    else
        q <= d;
end

endmodule
```

When `async_reset` is asserted, the output `q` becomes `0` immediately, independent of the clock.

The reset is therefore sensitive to its own transition as well as the clock.

---

## 3.2 Asynchronous Set D Flip-Flop

An asynchronous set forces the output to `1` independently of the clock.

Example:

```verilog
module dff_async_set (
    input clk,
    input async_set,
    input d,
    output reg q
);

always @(posedge clk, posedge async_set)
begin
    if (async_set)
        q <= 1'b1;
    else
        q <= d;
end

endmodule
```

When `async_set` is asserted, the output `q` becomes `1` without waiting for the next clock edge.

---

## 3.3 Synchronous Reset D Flip-Flop

A synchronous reset is checked only at the active clock edge.

Example:

```verilog
module dff_syncres (
    input clk,
    input sync_reset,
    input d,
    output reg q
);

always @(posedge clk)
begin
    if (sync_reset)
        q <= 1'b0;
    else
        q <= d;
end

endmodule
```

The reset affects the output only when the active clock edge occurs.

---

## 3.4 Asynchronous and Synchronous Reset Comparison

The difference can be represented as:

```text
Asynchronous Reset

Reset ─────────────► Output changes immediately


Synchronous Reset

Reset ─────► Clock Edge ─────► Output changes
```

| Feature | Asynchronous Reset | Synchronous Reset |
|---|---|---|
| Reset timing | Independent of clock | Dependent on clock |
| Output response | Immediate when reset is asserted | Changes at active clock edge |
| Sensitivity | Reset and clock | Clock |
| Typical use | Immediate reset requirements | Clock-controlled reset |

---

# 4. Simulation and Synthesis

The flip-flop designs were first verified through RTL simulation and then synthesized using Yosys.

---

## 4.1 Icarus Verilog Simulation

The RTL design and testbench were compiled using Icarus Verilog.

Example:

```bash
iverilog dff_asyncres.v tb_dff_asyncres.v
```

The simulation was then executed using:

```bash
./a.out
```

The generated waveform can be opened using GTKWave:

```bash
gtkwave tb_dff_asyncres.vcd
```

### 📷 Simulation Result

![Asynchronous Reset Waveform](https://github.com/user-attachments/assets/e971737d-85bb-4b78-983a-27dd0c5a2af4)

The waveform shows the relationship between the clock, reset, input data and flip-flop output.

For the asynchronous reset design, the output responds to the reset signal without waiting for a clock edge. When reset is inactive, the flip-flop follows the input data at the active clock edge.

---

## 4.2 Yosys Synthesis

Yosys was used to synthesize the flip-flop RTL and map it to the SKY130 standard-cell library.

Launch Yosys:

```bash
yosys
```

Read the technology library:

```bash
read_liberty -lib /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
```

Read the RTL design:

```bash
read_verilog /path/to/dff_asyncres.v
```

Select the top module and perform synthesis:

```bash
synth -top dff_asyncres
```

Map the flip-flop to a suitable library cell:

```bash
dfflibmap -liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
```

Perform technology mapping:

```bash
abc -liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
```

Display the synthesized circuit:

```bash
show
```

---

## 4.3 Yosys Command Summary

| Command | Purpose |
|---|---|
| `read_liberty` | Loads the standard-cell library |
| `read_verilog` | Reads the RTL design |
| `synth -top` | Performs synthesis |
| `dfflibmap` | Maps flip-flops to library cells |
| `abc` | Performs technology mapping |
| `show` | Displays the synthesized circuit |

---

## 4.4 Gate-Level Representation

After synthesis and technology mapping, the RTL flip-flop is represented using cells from the SKY130 standard-cell library.

### 📷 Synthesized Gate-Level Circuit

![Gate-Level Representation](https://github.com/user-attachments/assets/b6aefb1f-9c47-4dcb-8233-5bf461664823)

The synthesized circuit demonstrates how the RTL flip-flop is converted into a technology-specific gate-level implementation.

---

# 5. Observations

| Experiment | Observation |
|---|---|
| SKY130 `.lib` file | Contains standard-cell functionality and timing information |
| Hierarchical synthesis | Preserves module hierarchy |
| Flattened synthesis | Removes module boundaries and combines the design |
| Hierarchical vs flattened | The two approaches provide different structural representations |
| Asynchronous reset DFF | Reset can change the output independently of the clock |
| Asynchronous set DFF | Set can force the output to `1` independently of the clock |
| Synchronous reset DFF | Reset affects the output at the active clock edge |
| Icarus Verilog | Used to simulate the RTL design |
| GTKWave | Used to analyze simulation waveforms |
| Yosys | Used for RTL synthesis |
| `dfflibmap` | Used for flip-flop library mapping |
| `abc` | Used for technology mapping |
| SKY130 mapping | RTL was converted into a technology-specific gate-level representation |

---

# 6. Conclusion

Module 2 provided practical understanding of **technology libraries, hierarchical and flattened synthesis, and flip-flop RTL coding styles**.

The SKY130 `.lib` file was examined to understand how technology-library information is used during synthesis. Hierarchical and flattened synthesis were compared to understand the difference between preserving module structure and combining the design into a flat representation.

Different flip-flop RTL coding styles were implemented, including asynchronous reset, asynchronous set and synchronous reset. The designs were simulated using **Icarus Verilog** and the resulting waveforms were analyzed using **GTKWave**.

Finally, **Yosys** was used to synthesize the RTL and perform technology mapping using the SKY130 standard-cell library.

The overall flow studied was:

```text
RTL Coding
     ↓
RTL Simulation
     ↓
GTKWave Verification
     ↓
Yosys Synthesis
     ↓
Flip-Flop Mapping
     ↓
Technology Mapping
     ↓
Gate-Level Representation
```

The circuit diagrams, waveform screenshots and synthesis results included in this module were obtained from my own Module 2 laboratory experiments.
