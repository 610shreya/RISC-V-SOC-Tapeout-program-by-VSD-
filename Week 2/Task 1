# Week 2 – BabySoC Fundamentals & Functional Modelling

---

## 🎯 Objective
The goal of this week is to build a **solid understanding of SoC fundamentals** and practice **functional modelling** of the BabySoC using open-source simulation tools like **Icarus Verilog** and **GTKWave**.  

This week is more focused on **theory and conceptual clarity** rather than RTL coding, but it sets the stage for future design and verification work.  

---

## 📘 Part 1 – Fundamentals of SoC Design

### 🔹 What is a System-on-Chip (SoC)?
A **System-on-Chip (SoC)** is an integrated circuit that contains **all essential parts of a computing system** on a single silicon chip.  
It eliminates the need for multiple separate chips, thereby reducing **power consumption, cost, and board space**, while also **improving performance**.

Traditionally, a computer system may look like this:

    +---------+     +---------+     +-------------+
    |   CPU   | --> | Memory  | --> | Peripherals |
    +---------+     +---------+     +-------------+
          \______________________________________/
                       Bus / Interconnect

In an SoC, all these components are tightly integrated into a **single piece of silicon**, making it more efficient and compact.

---

### 🔹 Components of a Typical SoC
| Component       | Function                                                                 |
|-----------------|---------------------------------------------------------------------------|
| **CPU / Core**  | The brain of the SoC. Executes instructions, manages control flow.        |
| **Memory**      | Provides fast data and instruction storage (SRAM, DRAM, cache, ROM).     |
| **Peripherals** | Interfaces to the outside world: UART, SPI, I2C, GPIO, timers, etc.      |
| **Interconnect**| Bus or Network-on-Chip (NoC) enabling CPU-memory-peripheral communication.|
| **Special Units** | Sometimes includes accelerators like DSP, GPU, or AI cores.            |

📌 In real-world SoCs, these blocks are extremely complex, but for learning purposes we use **simplified SoCs** like BabySoC.  

---

### 🔹 Why BabySoC?
BabySoC is a **teaching SoC model** that reduces the system down to a minimal configuration while still representing the essential ideas of a full SoC.

**Key Reasons for BabySoC:**
1. **Simplicity** – Only includes a CPU, a small memory, and very few peripherals.  
2. **Focus** – Lets students concentrate on **concepts** (interconnects, functionality) instead of implementation details.  
3. **Approachability** – Easy to simulate with open-source tools like Icarus Verilog and GTKWave.  
4. **Foundation** – Acts as a stepping stone toward understanding complex designs like RISC-V SoCs.  

In short, BabySoC is **not meant for real products**, but it is perfect for **education and exploration**.  

---

### 🔹 BabySoC Block Diagram (Simplified)

    +-------------------+
    |      CPU Core     |
    +-------------------+
              |
              | Instruction / Data
              v
    +-------------------+
    |      Memory       |
    |   (SRAM / ROM)    |
    +-------------------+
              |
              | Bus / Interconnect
              v
    +-------------------+
    |   Peripherals     |
    | (UART, GPIO etc.) |
    +-------------------+

This **minimal model** reflects the **core concepts** of an SoC without overwhelming complexity.  

---

### 🔹 Role of Functional Modelling
Before jumping into **RTL design or physical design**, engineers often create **functional models**.  

**Functional modelling** means representing the **intended behavior** of a system without worrying about **timing delays, gate-level details, or PDK libraries**. It answers the question:  
👉 *“Does the system do what it is supposed to do?”*  

**Importance:**
- Helps validate **system architecture** before expensive design steps.  
- Enables **early debugging** of system-level issues.  
- Provides a **reference model** against which RTL can later be compared.  

**In BabySoC:**
- Functional models allow simulating CPU instructions, memory read/writes, and simple peripheral communication.  
- We can run **testbenches in Icarus Verilog**, capture waveforms in **GTKWave**, and confirm correctness.  

---

## 📝 Deliverable
This README serves as the **Week 2, Part 1 submission**.  
It provides a **2-page summary** covering:
- Fundamentals of SoC design  
- Core components of SoC  
- Relevance of BabySoC for beginners  
- Importance of functional modelling in the design flow  

In Part 2, we will extend this understanding by writing **functional testbenches** for BabySoC in Verilog and observing system-level interactions through simulation.

---

## 📚 References
- [Fundamentals of SoC Design (GitHub Notes)](https://github.com/hemanthkumardm/SFAL-VSD-SoC-Journey/tree/main/11.%20Fundamentals%20of%20SoC%20Design)  
- VLSI System Design (VSD) SoC Learning Journey  
- Textbook: *Computer Organization and Design – RISC-V Edition* by David Patterson & John Hennessy  

---
