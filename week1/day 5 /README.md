# Day 5 - Optimization in Synthesis: If-Case Constructs and For Loops

---

## 1. Introduction
Day 5 focuses on **synthesis optimizations** using **if-case constructs**, **for loops**, and **generate statements**.  
We explore how coding style affects the synthesized netlist and resource usage.

**Key Concepts:**
- **Incomplete if/case constructs:** May lead to inferred latches  
- **Overlapping case statements:** Can cause unintended behavior  
- **For loops & generate statements:** Efficient RTL replication and resource sharing  

---

## 2. Lab 10: Incomplete If / Case Constructs

**Objective:** Observe synthesis issues with incomplete if/case statements.

### Example Verilog (Incomplete If)
~~~~verilog
module incomplete_if(input a, b, output reg y);
    always @(*) begin
        if(a)
            y = b;
        // No else branch → may infer latch
    end
endmodule
~~~~

### Example Verilog (Overlapping Case)
~~~~verilog
module overlapping_case(input [1:0] sel, input a, b, output reg y);
    always @(*) begin
        case(sel)
            2'b00: y = a;
            2'b00: y = b; // Overlapping case
        endcase
    end
endmodule
~~~~

### Yosys Script (if_case_synth.ys)
~~~~tcl
# Load RTL
read_verilog incomplete_if.v overlapping_case.v

# Synthesize top modules
synth -top incomplete_if
synth -top overlapping_case

# Optimize logic
opt

# Map to standard cells
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80.lib

# Write synthesized netlists
write_verilog incomplete_if_synth.v
write_verilog overlapping_case_synth.v

# Visualize schematics
show
~~~~

### Commands
~~~~bash
yosys if_case_synth.ys
~~~~

**Notes:**
- Incomplete if/case can **infer unintended latches**  
- Overlapping case statements can **produce unpredictable outputs**  
- Always provide **complete coverage** in conditional constructs  

---

## 3. Lab 11: For Loops and Generate Statements

**Objective:** Learn efficient RTL replication using for loops and generate blocks.

### Example Verilog (For Loop)
~~~~verilog
module for_loop_example(input [3:0] a, output [3:0] b);
    genvar i;
    generate
        for(i=0; i<4; i=i+1) begin : loop_block
            assign b[i] = ~a[i]; // Invert each bit
        end
    endgenerate
endmodule
~~~~

### Yosys Script (for_loop_synth.ys)
~~~~tcl
# Load RTL
read_verilog for_loop_example.v

# Synthesize top module
synth -top for_loop_example

# Optimize logic
opt

# Map to standard cells
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80.lib

# Write synthesized netlist
write_verilog for_loop_synth.v

# Visualize schematic
show
~~~~

### Commands
~~~~bash
yosys for_loop_synth.ys
~~~~

**Notes:**
- `for` loops and `generate` blocks allow **compact RTL coding**  
- Reduces **manual instantiation** of repetitive logic  
- Synthesized hardware maps efficiently to multiple gates  

---

## 4. Summary

| Lab | Tool | Outcome |
|-----|------|--------|
| Lab 10 | Incomplete If / Case | Demonstrated latch inference and overlapping case issues |
| Lab 11 | For Loops / Generate | Efficient RTL replication and optimized netlist |

**Key Takeaways:**
- Always write **complete if/case constructs** to avoid latches  
- Overlapping case statements can create unpredictable outputs  
- For loops and generate statements simplify repetitive RTL and optimize synthesis
reness of synthesis-simulation mismatches improves design reliability

