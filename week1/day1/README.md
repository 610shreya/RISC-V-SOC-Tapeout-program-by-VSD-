# Day 1 - Lab 1: Introduction to Verilog RTL Design and Synthesis

## 1. Introduction
- Basics of RTL design
- Importance of simulation and synthesis
- Overview of open-source EDA tools

---

## 2. Lab 1: Icarus Verilog & GTKWave
- **Objective:** Simulate Verilog code
- **Tools:** Icarus Verilog, GTKWave
- **Steps & Commands:**

| Step | Command | Output |
|------|---------|--------|
| Compile | `iverilog -o design_tb.out design.v tb.v` | Generates executable |
| Simulate | `vvp design_tb.out` | Produces `dump.vcd` |
| View Waveform | `gtkwave dump.vcd` | Opens waveform GUI |

---

## 3. Lab 2: Introduction to Yosys
- **Objective:** Logic synthesis of RTL
- **Tools:** Yosys
- **Steps & Commands:**

| Step | Command | Output |
|------|---------|--------|
| Read design | `read_verilog design.v` | Loads RTL |
| Synthesize | `synth -top design` | Generates gate-level netlist |
| Optimize | `opt` | Optimizes logic |
| Write netlist | `write_verilog synth.v` | Saves synthesized design |
| Visualize | `show` | Schematic viewer |

---

## 4. Lab 3: Yosys + Sky130 PDK (2:1 MUX)
- **Objective:** Map RTL to standard cells
