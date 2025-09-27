# Day 2 - Timing Libraries, Hierarchical vs Flat Synthesis, Efficient Flop Coding Styles

---

## 1. Introduction
Day 2 focuses on **timing libraries**, **synthesis styles**, and **efficient flop coding**.  
We explore how RTL maps to standard cells with timing constraints, and how coding style affects synthesis and optimization.

**Key Concepts:**
- **Timing Libraries (`.lib`)** → Defines standard cell delays, setup/hold times, and drive strengths  
- **Hierarchical vs Flat Synthesis** → Design structure choices for synthesis  
- **Flop Coding Styles** → Efficient ways to describe flip-flops for optimized synthesis  

---

## 2. Lab 4: Introduction to `.lib` Timing Libraries

**Objective:** Understand timing library format and usage in synthesis.

**Tools:**  
- Yosys (synthesis)  
- Sky130 `.lib` files

### Steps & Commands
~~~~bash
# Inspect timing library
cat sky130_fd_sc_hd__tt_025C_1v80.lib

# Optional: parse in Yosys
yosys
yosys> read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
yosys> show
~~~~

**Notes:**
- `.lib` files define **cell delays**, **timing arcs**, and **constraints**.  
- Timing-aware synthesis uses these values to generate **timing-optimized netlists**.

---

## 3. Lab 5: Hierarchical vs Flat Synthesis & Flop Coding Styles

**Objective:** Explore the impact of design structure and flop coding on synthesis and optimization.

**Topics Covered:**
- **Hierarchical vs Flat Synthesis**
  | Style | Description | Pros | Cons |
  |-------|------------|------|------|
  | Hierarchical | Preserves module hierarchy during synthesis | Easier debug, modular | Slightly slower optimization |
  | Flat | Flattens all modules into single netlist | Max optimization | Harder debug, larger netlist |

- **Flop Coding Styles**
  | Style | Description | Use |
  |-------|------------|-----|
  | Always block with posedge | Standard sequential flop | Most common |
  | Non-blocking assignments | Ensures proper RTL simulation | Recommended for multi-flop chains |
  | Clock gating | Reduces dynamic power | Power optimization |
  
- **Why Flops Matter:**  
  Flops determine **timing paths** and **pipeline behavior**; coding style affects area, timing, and power.

---

## 4. Lab 5: Flop Synthesis and Optimization

**Objective:** Synthesize various flop coding styles and observe optimizations.

### Example Verilog Flops
~~~~verilog
// Simple D flip-flop
module dff_simple(input clk, d, output reg q);
  always @(posedge clk)
    q <= d;
endmodule

// Clock-gated flip-flop
module dff_clock_gated(input clk, en, d, output reg q);
  wire gated_clk = clk & en;
  always @(posedge gated_clk)
    q <= d;
endmodule
~~~~

### Yosys Synthesis Script (flop_synth.ys)
~~~~tcl
# Load RTL
read_verilog dff_simple.v dff_clock_gated.v

# Set top module
synth -top dff_simple

# Optimize logic
opt

# Map to standard cells
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80.lib

# Write synthesized netlist
write_verilog dff_synth.v

# Visualize schematic
show
~~~~

### Commands
~~~~bash
# Run Yosys synthesis
yosys flop_synth.ys
~~~~

**Interesting Optimizations:**
- Flattening small modules may improve timing  
- Clock gating reduces dynamic power  
- Non-blocking assignments ensure correct flop behavior in synthesis

---

## 5. Summary

| Lab | Tool | Outcome |
|-----|------|--------|
| Lab 4 | Timing libraries `.lib` | Understanding cell delays and constraints |
| Lab 5 | Hierarchical vs Flat Synthesis | Compare netlist optimization, debug ease |
| Lab 5 | Flop Coding Styles | Synthesized flop netlists, optimized timing and power |

**Key Takeaways:**
- Timing libraries are crucial for timing-aware synthesis  
- Hierarchical vs Flat synthesis affects optimization and debug  
- Flop coding style impacts area, timing, and power efficiency

