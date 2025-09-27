# Day 1 - Lab 1: Introduction to Verilog RTL Design and Synthesis

---

## 1. Introduction
RTL (Register Transfer Level) design is the process of describing the **digital circuit’s behavior** using registers and combinational logic.  
Simulation and synthesis are essential steps to validate and implement designs.

**Key Concepts:**
- **RTL Design:** Describes data flow between registers and logic operations
- **Simulation:** Verifies functional correctness before hardware implementation
- **Synthesis:** Converts RTL into a gate-level netlist using standard cell libraries
- **Open-Source Tools:** Icarus Verilog, GTKWave, Yosys, Sky130 PDK

---

## 2. Lab 1: Icarus Verilog & GTKWave

**Objective:** Compile and simulate Verilog code using open-source tools.

**Tools Required:**
| Tool | Purpose |
|------|---------|
| Icarus Verilog (`iverilog`) | Compile and simulate Verilog RTL |
| GTKWave | Visualize waveform (`.vcd`) files |

**Steps & Commands:**
| Step | Command | Output / Notes |
|------|---------|----------------|
| Write RTL & Testbench | `design.v` & `tb.v` | Define module and test scenarios |
| Compile design | `iverilog -o design_tb.out design.v tb.v` | Generates executable `design_tb.out` |
| Run simulation | `vvp design_tb.out` | Produces waveform dump `dump.vcd` |
| View waveform | `gtkwave dump.vcd` | Opens waveform GUI for verification |

**Example Verilog (2:1 MUX):**
```verilog
module mux2x1(input a, b, sel, output y);
  assign y = sel ? b : a;
endmodule
