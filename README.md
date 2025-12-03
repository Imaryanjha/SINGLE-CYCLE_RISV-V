# FPGA Design & Simulation Hackathon: Systolic Array RTL Exploration

## Project Overview
This project involves the design, simulation, and verification of a **4x4 Systolic Array** for matrix multiplication, implemented in Verilog and targeted for FPGA synthesis. The design is fully parameterized, pipelined, and includes saturation logic to prevent overflow.

---

## Team Members
- **Aryan Raj**
- **Siddharth Penumatsa**

---

## Key Features
- **4x4 Systolic Array** with 16 Processing Elements (PEs)
- **Output-Stationary Dataflow**
- **Parameterized Design** (scalable to 2x2, 8x8, 16x16, etc.)
- **Pipelined Processing** with registered I/O
- **16-bit Saturated Output** from 20-bit internal accumulators
- **Fixed Latency** of 10 clock cycles
- **Automated RTL-to-Netlist Flow** on Windows

---

## Design Specifications
### Data Types
- **Inputs (A, B):** 8-bit signed integers
- **Internal Accumulator:** 20-bit signed
- **Output (C):** 16-bit signed (saturated)

### Control Signals
- `clk`, `rst`: Clock and reset
- `clr`: Clear accumulator before new calculation
- `a_v_in`, `b_v_in`: Input valid signals
- `do_acc`: ANDed valid signal for accumulation enable
- `done`: Calculation completion signal

---

## Architecture
### Processing Element (PE) Design
Each PE performs:
- **Multiply-Accumulate (MAC)** operation
- **Registered I/O** for pipelining
- **Saturation** before output

### Systolic Array Structure
- **Flattened I/O** for tool compatibility
- **Generate blocks** for mesh instantiation
- **Wavefront data feeding** mimicking systolic flow

---

## Verification Strategy
### Golden Model
- Software-based reference model for expected results
- Behavioral Verilog loops for matrix multiplication

### Testbench Features
- Skewed matrix input generation
- Latency-aware valid signal control
- Automatic result comparison (PASS/FAIL reporting)

---

## Simulation Environment
### Tools Used
- **Editor & Automation:** VS Code with PowerShell scripts
- **Simulator:** Icarus Verilog (iverilog)
- **Waveform Viewer:** Surfer
- **Synthesizer:** Yosys + ABC
- **Netlist Visualization:** NetlistsVG via Node.js

### Automated Flow
- Single keystroke (`Ctrl+Shift+B`) runs:
  1. RTL Compilation
  2. Simulation
  3. Waveform Generation
  4. Synthesis
  5. Report Generation (Area, Timing, Cells)
  6. Netlist Visualization

---

## Results
- ✅ **Fully Verified** against golden model
- ✅ **Parameterized & Scalable** design
- ✅ **Pipelined Operation** confirmed via waveforms
- ✅ **Fixed Latency** of 10 cycles achieved
- ✅ **Saturation Logic** functioning correctly
- ✅ **Automated Flow** reusable for future projects

---

## Key Learnings
1. **Valid Signal Timing:** Must remain high for entire latency (`K+N-1+N-1` cycles)
2. **Tool Compatibility:** Use packed arrays for port compatibility with Yosys
3. **Automation Value:** Local automated flow reduces dependency on cloud platforms
4. **Modular Design:** Enables easy scaling and reuse

---

## Repository Structure



```
├── alu.v
├── alu_control.v
├── alu_tb.v
├── control_unit.v
├── control_tb.v
├── datapath.v
├── datapath_tb.v
├── generate_riscv_schematic.sh
├── imm_gen.v
├── imm_gen_tb.v
├── quick.png
├── regfile.v
├── regfile_tb.v
├── riscv_cpu.v
├── riscv_schematic.dot
├── riscv_schematic.png
├── riscv_visualization.m
├── simple_riscv_visulization.m
├── synthesize.ys
└── yosys_stats.txt

```
