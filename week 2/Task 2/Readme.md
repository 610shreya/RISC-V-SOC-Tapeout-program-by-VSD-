# Week 2 – BabySoC Fundamentals & Functional Modelling  
**Part 2 – Labs (Hands-on Functional Modelling)**  

---

## 🎯 Objective  
To build a **solid understanding of SoC fundamentals** and practice **functional modelling of BabySoC** using simulation tools:  
- **Icarus Verilog (iverilog)** for compiling and simulating Verilog code.  
- **GTKWave** for viewing and analyzing waveform files.  

---

## 🧪 Lab Reference  
[VSDBabySoC Project Labs](https://github.com/hemanthkumardm/SFAL-VSD-SoC-Journey/tree/main/12.%20VSDBabySoC%20Project)  

---

## ⚙️ Tools Required  
- **Icarus Verilog** → Verilog compiler & simulator  
- **GTKWave** → Waveform viewer  

---

## 📝 Lab Steps  

1. **Clone the BabySoC project repository**  
    ```bash
    git clone https://github.com/hemanthkumardm/SFAL-VSD-SoC-Journey.git
    cd SFAL-VSD-SoC-Journey/12.\ VSDBabySoC\ Project
    ```

2. **Compile the BabySoC Verilog modules**  
    ```bash
    iverilog -o baby_soc_tb.vvp baby_soc_tb.v
    ```

3. **Simulate and generate .vcd waveform files**  
    ```bash
    vvp baby_soc_tb.vvp
    ```

4. **Open .vcd files in GTKWave and analyze:**  
    - Reset operation  
    - Clock signals  
    - Dataflow between CPU, Memory, and Peripherals  

5. **Document your observations with screenshots of waveforms**  

---

## 📊 Deliverables  

- **Simulation logs** (output from compilation & simulation)  
- **GTKWave screenshots** highlighting correct BabySoC behavior:  
  - Reset operation  
  - Clocking  
  - Dataflow between modules  

- **Short explanation for each screenshot**, describing what the waveform represents.  

---

## 📚 Example Template  

**Simulation Log Snippet:**  
```
$ iverilog -o baby_soc_tb.vvp baby_soc_tb.v
$ vvp baby_soc_tb.vvp
VCD info: dumpfile dump.vcd opened for output.
```

---

✅ This completes **Week 2, Part 2 submission**.  
Replace the placeholders with your **actual logs and GTKWave screenshots** before pushing to GitHub.
