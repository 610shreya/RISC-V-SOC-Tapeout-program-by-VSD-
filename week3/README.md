# Week 3 – Post-Synthesis GLS & STA Fundamentals  

---

## 🎯 Objective  
To understand and perform **Gate-Level Simulation (GLS)** after synthesis, validate design functionality, and get introduced to **Static Timing Analysis (STA)** concepts with practical experiments using **OpenSTA**.

---

# 🧩 Part 1 – Post-Synthesis Gate-Level Simulation (GLS)  

### 🔗 Reference  
[VSD_HDP – Day 6 Example](https://github.com/Ananya-KM/VSD_HDP/blob/main/Day%206.md)

### ⚙️ Tools Used  
| Tool | Purpose |
|------|----------|
| **Yosys** | Logic synthesis (to generate gate-level netlist) |
| **Icarus Verilog (iverilog)** | GLS simulation |
| **GTKWave** | Waveform viewer |

---

### 🧪 Steps  

1️⃣ **Run Synthesis using Yosys**
```bash
yosys
yosys> read_verilog baby_soc.v
yosys> synth -top baby_soc
yosys> write_verilog baby_soc_netlist.v
yosys> write_sdf baby_soc_timing.sdf
```

Outputs:  
- `baby_soc_netlist.v` → synthesized gate-level netlist  
- `baby_soc_timing.sdf` → optional timing data  

---

2️⃣ **Run Gate-Level Simulation**
```bash
iverilog -o baby_soc_gls.vvp baby_soc_netlist.v baby_soc_tb.v
vvp baby_soc_gls.vvp
```
Generates `dump.vcd` waveform file.

---

3️⃣ **View in GTKWave**
```bash
gtkwave dump.vcd
```
Verify:  
- ✅ Reset operation  
- ✅ Clock generation  
- ✅ Data flow between CPU ↔ Memory ↔ Peripherals  

---

### 📊 Deliverables  

| Deliverable | Description |
|--------------|--------------|
| **Synthesis Logs** | Output logs from Yosys |
| **GLS Waveforms** | Screenshots showing post-synthesis behavior |
| **Verification Note** | Confirm GLS = Functional outputs |

---

### 🧾 Example  

**Synthesis Log:**  
```
-- Yosys synthesis completed successfully
-- Writing netlist: baby_soc_netlist.v
```

**Simulation Log:**  
```
$ vvp baby_soc_gls.vvp
VCD info: dumpfile dump.vcd opened for output.
```

**Screenshots:**  
1️⃣ Reset behavior → CPU held in reset, then released.  
2️⃣ Clock signal → Clean periodic toggling.  
3️⃣ Data flow → Matches Week 2 functional simulation.  

✅ GLS outputs **match** functional results → Synthesis preserves logic.

---

# 🧠 Part 2 – Fundamentals of STA (Static Timing Analysis)  

### 🔗 Reference  
[STA Fundamentals – Udemy Course](https://www.udemy.com/course/vlsi-academy-stachecks/?couponCode=F960AEDD365E0CD12546)

### 🎓 Key Topics  
- Setup and Hold Checks  
- Slack (Positive / Negative)  
- Clock Definitions and Domains  
- Path-Based Timing Analysis  

---

### 🗒️ Deliverable – One-Page Summary (Example Template)

**STA Fundamentals – Key Notes**  
- **Setup Check:** Ensures data arrives *before* the clock edge → no timing violation.  
- **Hold Check:** Ensures data remains stable *after* the clock edge.  
- **Slack = Required Time − Arrival Time.**  
  - Positive Slack → meets timing.  
  - Negative Slack → violation exists.  
- **Clock Definition:** Primary clock signal driving flip-flops; multiple clock domains must be defined for STA.  
- **Path Analysis:** Analyzes timing from start point (launch FF) to end point (capture FF).  
- **Critical Path:** Longest path with least slack → determines max frequency.  
- **Hold Fixes:** Insert delay buffers or adjust clock skew.  
- **Setup Fixes:** Reduce logic depth or increase clock period.  

---

# ⚡ Part 3 – Generate Timing Graphs with OpenSTA  

### 🔗 References  
- [OpenSTA GitHub](https://github.com/The-OpenROAD-Project/OpenSTA)  
- [Example Script – Day 19](https://github.com/arunkpv/vsd-hdp/blob/main/docs/Day_19.md)  
- [OpenSTA Documentation (PDF)](https://github.com/The-OpenROAD-Project/OpenSTA/blob/master/doc/OpenSTA.pdf)

---

### 🧪 Steps  

1️⃣ **Load Netlist and Constraints**
```bash
read_verilog baby_soc_netlist.v
read_liberty sky130_fd_sc_hd__tt_025C_1v80.lib
read_sdc constraints.sdc
link_design baby_soc
```

2️⃣ **Run Timing Analysis**
```bash
report_checks -path_delay min_max
report_timing -max_paths 5
```

3️⃣ **Generate Timing Graphs**
```bash
report_tns
report_wns
```
Capture output and graphs (show slack and critical path).

---

### 📊 Deliverables  

| Deliverable | Description |
|--------------|-------------|
| **OpenSTA Input Scripts** | `.tcl` files used to run timing analysis |
| **Timing Reports & Graphs** | Screenshots with user ID & timestamp |
| **Observations** | Identify critical path & interpret slack values |

---

### 🧾 Example Output  

**OpenSTA Run Log:**
```
report_timing
Startpoint: cpu_reg[3] (rising edge-triggered flip-flop)
Endpoint: mem_reg[1]
Path slack: +0.21 ns
```

**Observation:**
- Critical path found between CPU register and Memory register.  
- Positive slack → Design meets timing.  

---

# ✅ Final Outcomes of Week 3  

By the end of Week 3, you will have:
1. Performed GLS and validated functional correctness post-synthesis.  
2. Gained fundamental understanding of STA (Setup, Hold, Slack).  
3. Generated timing graphs with OpenSTA and interpreted critical paths.  

---

# 📁 Recommended Folder Structure  

```
Week3/
 ├── Part1_PostSynthesis_GLS/
 │    ├── baby_soc_netlist.v
 │    ├── logs/
 │    │    └── synthesis_log.txt
 │    ├── waveforms/
 │    │    └── dump.vcd
 │    ├── screenshots/
 │    │    ├── reset_waveform.png
 │    │    └── dataflow_waveform.png
 │    └── README.md
 ├── Part2_STA_Fundamentals/
 │    └── sta_notes.md
 └── Part3_OpenSTA_Timing/
      ├── scripts/
      │    └── timing_analysis.tcl
      ├── reports/
      │    └── timing_report.txt
      ├── screenshots/
      │    ├── critical_path.png
      │    └── slack_report.png
      └── README.md
```

---

💡 **Tip:**  
Commit logs, screenshots, and scripts separately for clean version control and easy evaluation.  
