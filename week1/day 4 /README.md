# Day 4 - Gate-Level Simulation (GLS), Blocking vs Non-blocking, and Synthesis-Simulation Mismatch

---

## 1. Introduction
Day 4 focuses on **Gate-Level Simulation (GLS)**, **blocking vs non-blocking statements**, and **synthesis-simulation mismatches**.

**Key Concepts:**
- **GLS (Gate-Level Simulation):** Validates synthesized netlist behavior  
- **Blocking (`=`) vs Non-blocking (`<=`) assignments:** Correct RTL modeling  
- **Synthesis-Simulation Mismatch:** Differences between RTL and synthesized netlist behavior  

---

## 2. Lab 8: GLS Concepts and Flow Using Icarus Verilog

**Objective:** Understand GLS and verify synthesized netlists.

### Example Verilog (Simple Netlist)
~~~~verilog
module and_gate(input a, b, output y);
    assign y = a & b;
endmodule

module tb_and_gate;
    reg a, b;
    wire y;
    and_gate uut(.a(a), .b(b), .y(y));

    initial begin
        $dumpfile("and_gate.vcd");
        $dumpvars(0, tb_and_gate);
        a=0; b=0; #10;
        a=0; b=1; #10;
        a=1; b=0; #10;
        a=1; b=1; #10;
        $finish;
    end
endmodule
~~~~

### Commands
~~~~bash
# Compile gate-level design
iverilog -o and_gate_gls.out and_gate.v tb_and_gate.v

# Run GLS
vvp and_gate_gls.out

# View waveform
gtkwave and_gate.vcd
~~~~

**Notes:**
- GLS ensures synthesized netlist matches RTL behavior  
- Useful for timing verification  

---

## 3. Lab 9: Synthesis-Simulation Mismatch & Blocking Statements

**Objective:** Demonstrate mismatch caused by improper use of blocking statements.

### Example Verilog (Blocking vs Non-blocking)
~~~~verilog
module flop_mismatch(input clk, d, output reg q_block, q_nonblock);
    always @(posedge clk) begin
        q_block = d;       // Blocking assignment
        q_nonblock <= d;   // Non-blocking assignment
    end
endmodule
~~~~

### Yosys Synthesis Script (mismatch_synth.ys)
~~~~tcl
# Load RTL
read_verilog flop_mismatch.v

# Synthesize top module
synth -top flop_mismatch

# Optimize logic
opt

# Map to standard cells
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80.lib

# Write synthesized netlist
write_verilog flop_mismatch_synth.v

# Visualize schematic
show
~~~~

### Commands
~~~~bash
# Run synthesis
yosys mismatch_synth.ys

# Optional: GLS simulation for synthesized netlist
iverilog -o flop_mismatch_gls.out flop_mismatch_synth.v tb_flop_mismatch.v
vvp flop_mismatch_gls.out
gtkwave flop_mismatch.vcd
~~~~

**Caveats with Blocking Statements:**
- Blocking assignments (`=`) may cause **simulation vs synthesis mismatch**  
- Non-blocking (`<=`) recommended for sequential logic to match RTL and gate-level timing  

---

## 4. Summary

| Lab | Tool | Outcome |
|-----|------|--------|
| Lab 8 | Icarus Verilog GLS | Verified gate-level netlist functionality |
| Lab 9 | Synthesis-Simulation Mismatch | Demonstrated RTL vs synthesized mismatch due to blocking assignments |

**Key Takeaways:**
- GLS is essential to validate synthesized netlists  
- Use non-blocking assignments for sequential logic  
- Awareness of synthesis-simulation mismatches improves design reliability

