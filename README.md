# RTL_Design_Workshop 
 
This repository documents my learning journey through RTL design, Verilog simulation, synthesis, timing libraries, sequential circuit design, Gate-Level Simulation (GLS), synthesis-simulation mismatch analysis, and optimization in synthesis. 
 
Each module contains the concepts studied, practical experiments, commands used, simulation results, synthesis results, screenshots, and observations from the workshop. 
 
--- 
 
## 📚 Workshop Progress 
 
| **Module** | **Topics Covered** | **Status** | 
|------------|--------------------|------------| 
| Module 1 | Verilog RTL Design, Icarus Verilog, GTKWave & Yosys Synthesis | ✅ Completed | 
| Module 2 | Timing Libraries, Synthesis Methods & Flip-Flop RTL Coding | ✅ Completed | 
| Module 3 | Combinational and Sequential Logic Optimizations | ✅ Completed | 
| Module 4 | GLS, Synthesis-Simulation Mismatch & Blocking/Non-Blocking Statements | ✅ Completed | 
| Module 5 | Optimization in Synthesis, IF/CASE Constructs & FOR Loop/Generate | ✅ Completed | 
 
--- 
 
## 📂 Repository Structure 
 
```text
RTL_Design_Workshop 
│ 
├── README.md 
│ 
├── module_1 
│   └── README.md 
│ 
├── module_2 
│   ├── README.md 
│   └── images/ 
│ 
├── module_3 
│   ├── README.md 
│   └── images/ 
│ 
├── module_4 
│   ├── README.md 
│   └── images/ 
│ 
└── module_5 
    ├── README.md 
    └── images/
``` 
 
--- 
 
# Module 1 – RTL Design, Simulation & Synthesis 
 
Module 1 focused on understanding the basic RTL design flow, starting with Verilog simulation and progressing towards synthesis using Yosys. 
 
### Topics Covered 
 
- Simulator, Design and Testbench 
- Icarus Verilog simulation 
- 2:1 Multiplexer implementation 
- GTKWave waveform analysis 
- RTL Design and Synthesis 
- Introduction to Yosys 
- Understanding `.lib` files 
- Faster and slower cell flavors 
- Cell selection based on design requirements 
- Yosys synthesis flow 
- Synthesis statistics 
- Gate-level representation 
- Generated gate-level netlist 
 
## 🔗 Module 1 Documentation 
 
➡️ [Module 1 – RTL Design, Simulation & Synthesis](./module_1/README.md) 
 
--- 
 
# Module 2 – Timing Libraries, Synthesis & Flip-Flop RTL 
 
Module 2 focused on understanding technology libraries, timing information, hierarchical and flattened synthesis, and flip-flop RTL coding styles. 
 
### Topics Covered 
 
- SKY130 technology library 
- Understanding `.lib` timing libraries 
- Process, voltage and temperature conditions 
- Hierarchical synthesis 
- Flattened synthesis 
- Comparison of hierarchical and flattened synthesis 
- Asynchronous reset D flip-flop 
- Asynchronous set D flip-flop 
- Synchronous reset D flip-flop 
- Icarus Verilog simulation 
- GTKWave waveform analysis 
- Yosys synthesis 
- `dfflibmap` for flip-flop mapping 
- Technology mapping using `abc` 
- Gate-level representation 
 
## 🔗 Module 2 Documentation 
 
➡️ [Module 2 – Timing Libraries, Synthesis & Flip-Flop RTL](./module_2/README.md) 
 
--- 
 
# Module 3 – Combinational and Sequential Logic Optimizations 
 
Module 3 focused on understanding RTL optimization and how combinational and sequential logic are optimized during synthesis. 
 
### Topics Covered 
 
- RTL optimization 
- Combinational logic optimization 
- AND logic 
- OR logic 
- Three-input logic 
- XNOR logic 
- Constant propagation 
- Sequential logic optimization 
- Counter optimization 
- Flip-flop optimization 
- Optimization of unused sequential logic 
- Yosys synthesis 
- SKY130 technology mapping 
- Icarus Verilog simulation 
- GTKWave waveform analysis 
 
## 🔗 Module 3 Documentation 
 
➡️ [Module 3 – Combinational and Sequential Logic Optimizations](./module_3/README.md) 
 
--- 
 
# Module 4 – GLS, Synthesis-Simulation Mismatch & Blocking/Non-Blocking Statements 
 
Module 4 focused on Gate-Level Simulation (GLS), synthesis-simulation mismatch, and the correct use of blocking and non-blocking assignments in Verilog. 
 
### Topics Covered 
 
- Gate-Level Simulation (GLS) 
- GLS concepts and flow 
- Synthesis-simulation mismatch 
- Blocking assignments 
- Non-blocking assignments 
- Caveats with blocking statements 
- Ternary operator and multiplexer implementation 
- GLS laboratory experiments 
- Synthesis-simulation mismatch experiments 
- Blocking statement mismatch experiments 
- Technology-specific simulation 
- Icarus Verilog 
- GTKWave 
- Yosys 
 
## 🔗 Module 4 Documentation 
 
➡️ [Module 4 – GLS, Synthesis-Simulation Mismatch & Blocking/Non-Blocking Statements](./module_4/README.md) 
 
--- 
 
# Module 5 – Optimization in Synthesis 
 
Module 5 focused on understanding how different Verilog RTL coding constructs affect synthesis and the resulting hardware implementation. 
 
### Topics Covered 
 
- RTL coding styles 
- IF-ELSE statements 
- Priority logic using IF-ELSE 
- CASE statements 
- Selection logic using CASE 
- IF-ELSE and CASE comparison 
- Incomplete IF statements 
- Incomplete CASE statements 
- Incomplete and overlapping CASE conditions 
- Partial CASE assignment 
- FOR loop 
- FOR generate 
- FOR loop and FOR generate comparison 
- Ripple Carry Adder (RCA) 
- Multiplexer using FOR generate 
- Comparator using CASE 
- Demultiplexer using CASE 
- Demultiplexer using FOR generate 
- Icarus Verilog simulation 
- GTKWave waveform analysis 
- Yosys synthesis 
- SKY130 technology mapping 
 
## 🔗 Module 5 Documentation 
 
➡️ [Module 5 – Optimization in Synthesis](./module_5/README.md) 
 
--- 
 
## 🛠 Tools Used 
 
- Verilog 
- Icarus Verilog (`iverilog`) 
- GTKWave 
- Yosys 
- SKY130 Standard Cell Library 
- Linux / Ubuntu 
- Git 
- GitHub 
 
--- 
 
## 📌 Key Learning Outcomes 
 
Through these modules, I gained practical understanding of: 
 
- RTL design using Verilog 
- Simulation and testbench development 
- Waveform analysis 
- RTL synthesis 
- Technology mapping 
- Timing libraries 
- Sequential circuit design 
- Combinational and sequential optimization 
- Gate-Level Simulation 
- Synthesis-simulation mismatch 
- Blocking and non-blocking coding styles 
- IF-ELSE and CASE based RTL coding 
- Incomplete and overlapping conditional logic 
- FOR loops and FOR generate constructs 
- Repetitive hardware structure generation 
- SKY130 standard-cell based design flow 
 
--- 
 
## 👩‍💻 Author 
 
**AISHWARYA NOMULA**
