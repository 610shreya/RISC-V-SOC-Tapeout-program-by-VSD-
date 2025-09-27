
# Day 3 - Combinational and Sequential Logic Optimizations

---

## 1. Introduction
Day 3 focuses on **optimizing combinational and sequential logic** for area, timing, and power efficiency.  
We explore **Yosys optimization techniques**, synthesis strategies, and handling unused outputs.

**Key Concepts:**
- **Combinational Logic Optimization:** Reduce logic depth and area  
- **Sequential Logic Optimization:** Optimize flip-flops and registers  
- **Unused Outputs:** Detect and remove for area and power reduction  

---

## 2. Lab 6: Combinational Logic Optimization

**Objective:** Optimize combinational circuits for area and timing.

**Tools:**  
- Yosys synthesis

### Example Verilog (Combinational Logic)
~~~~verilog
module comb_logic(input a, b, c, output y1, y2);
  assign y1 = (a & b) | (~c);
  assign y2 = (a & c) | (b & ~c);
endmodule
~~~~

### Yosys Script (comb_opt.ys)
~~~~tcl
# Load RTL
read_verilog comb_logic.v

# Synthesize top module
synth -top comb_logic

# Optimize combinational logic
opt

# Map to standard cells
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80.lib

# Write optimized netlist
write_verilog comb_logic_opt.v

# Visualize schematic
show
~~~~

### Commands
~~~~bash
# Run Yosys combinational optimization
yosys comb_opt.ys
~~~~

**Notes:**
- `opt` reduces logic depth, removes redundant logic  
- Useful for timing-critical combinational paths  

---

## 3. Lab 7: Sequential Logic Optimization

**Objective:** Optimize sequential circuits and handle unused outputs.

**Tools:**  
- Yosys synthesis

### Example Verilog (Sequential Logic)
~~~~verilog
module seq_logic(input clk, rst, d1, d2, output reg q1, q2, q3_unused);
  always @(posedge clk or posedge rst) begin
    if(rst) begin
      q1 <= 0;
      q2 <= 0;
      q3_unused <= 0;
    end else begin
      q1 <= d1;
      q2 <= d2;
      q3_unused <= q1 & q2; // Unused output
    end
  end
endmodule
~~~~

### Yosys Script (seq_opt.ys)
~~~~tcl
# Load RTL
read_verilog seq_logic.v

# Synthesize top module
synth -top seq_logic

# Optimize sequential logic
opt

# Detect and remove unused outputs
clean

# Map to standard cells
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80.lib

# Write optimized netlist
write_verilog seq_logic_opt.v

# Visualize schematic
show
~~~~

### Commands
~~~~bash
# Run Yosys sequential optimization
yosys seq_opt.ys
~~~~

**Interesting Optimizations:**
- Unused outputs removed with `clean`  
- Sequential optimizations reduce flop area and timing paths  
- Ensures pipeline efficiency  

---

## 4. Summary

| Lab | Tool | Outcome |
|-----|------|--------|
| Lab 6 | Combinational Logic Optimization | Optimized combinational netlist `comb_logic_opt.v` |
| Lab 7 | Sequential Logic Optimization | Optimized sequential netlist `seq_logic_opt.v`, unused outputs removed |

**Key Takeaways:**
- `opt` and `clean` in Yosys effectively reduce area and timing  
- Sequential logic optimization improves pipeline performance  
- Removing unused outputs reduces area and power
