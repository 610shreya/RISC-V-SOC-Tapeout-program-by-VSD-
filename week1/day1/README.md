# Day 1 - Lab 1: Introduction to Verilog RTL Design and Synthesis

---

## 1. Introduction
RTL (Register Transfer Level) design describes the behavior of digital circuits at the register and combinational logic level.  
Simulation and synthesis are key steps for validating and implementing designs.

**Key Tools:**
- **Icarus Verilog** → Compile & simulate RTL  
- **GTKWave** → View waveforms  
- **Yosys** → Logic synthesis  
- **Sky130 PDK** → Standard cell mapping

---

## 2. Lab 1: Icarus Verilog & GTKWave

**Objective:** Compile and simulate Verilog RTL using open-source tools.

### Verilog Example (2:1 MUX)
~~~~verilog
module mux2x1(input a, b, sel, output y);
    assign y = sel ? b : a;
endmodule

module tb_mux2x1;
    reg a, b, sel;
    wire y;

    mux2x1 uut(.a(a), .b(b), .sel(sel), .y(y));

    initial begin
        $dumpfile("mux.vcd");
        $dumpvars(0, tb_mux2x1);
        a=0; b=0; sel=0; #10;
        a=0; b=1; sel=1; #10;
        a=1; b=0; sel=0; #10;
        a=1; b=1; sel=1; #10;
        $finish;
    end
endmodule
~~~~

### Commands
~~~~bash
# Compile the design
iverilog -o mux_tb.out mux.v

# Run simulation
vvp mux_tb.out

# View waveform
gtkwave mux.vcd
~~~~

---

## 3. Lab 2: Yosys Logic Synthesis

**Objective:** Synthesize RTL to gate-level netlist.

### Yosys Script (synth.ys)
~~~~tcl
# Load RTL design
read_verilog mux.v

# Set top module
synth -top mux2x1

# Optimize logic
opt

# Write synthesized netlist
write_verilog mux_synth.v

# Visualize schematic
show
~~~~

### Commands
~~~~bash
# Run Yosys with the script
yosys synth.ys
~~~~

---

## 4. Lab 3: Yosys + Sky130 PDK Mapping

**Objective:** Map synthesized design to Sky130 standard cells.

### Sky130 Mapping Script (map_sky130.ys)
~~~~tcl
# Load RTL
read_verilog mux.v

# Synthesize RTL
synth -top mux2x1

# Optimize
opt

# Load Sky130 standard cell library
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib

# Map cells
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80.lib

# Write gate-level netlist mapped to Sky130
write_verilog mux_sky130.v

# Visualize mapped schematic
show
~~~~

### Commands
~~~~bash
# Run Yosys with Sky130 mapping
yosys map_sky130.ys
~~~~

---

## 5. Summary

| Lab | Tool | Output |
|-----|------|--------|
| Lab 1 | Icarus Verilog + GTKWave | Simulated RTL, waveform `mux.vcd` |
| Lab 2 | Yosys | Gate-level netlist `mux_synth.v` |
| Lab 3 | Yosys + Sky130 PDK | Gate-level netlist mapped to Sky130 `mux_sky130.v` |

**Key Takeaways:**
- Simulate RTL designs with Icarus Verilog  
- View waveforms with GTKWave  
- Synthesize RTL using Yosys  
- Map RTL to standard cells using Sky130 PDK
