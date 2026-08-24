# Module 2 – Timing Libraries, Synthesis & Flip-Flop RTL

## 🎯 Experiment Objective

The objective of Module 2 was to understand **technology libraries and timing information**, study **hierarchical and flattened synthesis**, and learn different methods of describing **flip-flops with reset and set conditions** using Verilog RTL.

The experiments also included simulation using **Icarus Verilog**, waveform analysis using **GTKWave**, and synthesis and technology mapping using **Yosys** with the SKY130 standard-cell library.

---

## 📑 Contents

- [1. Technology Libraries](#1-technology-libraries)
- [2. Hierarchical and Flattened Synthesis](#2-hierarchical-and-flattened-synthesis)
- [3. Flip-Flop RTL Coding](#3-flip-flop-rtl-coding)
- [4. Simulation and Synthesis](#4-simulation-and-synthesis)
- [5. Observations](#5-observations)
- [6. Conclusion](#6-conclusion)

---

# 1. Technology Libraries

A technology library contains information about the standard cells available for a particular semiconductor technology.

The library provides information such as:

- Cell functionality
- Timing characteristics
- Power information
- Operating conditions
- Standard-cell descriptions

The SKY130 library used in this experiment was:

```text
sky130_fd_sc_hd__tt_025C_1v80.lib
