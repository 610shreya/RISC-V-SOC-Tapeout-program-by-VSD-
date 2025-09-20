# Week 0 — Setup & Tools

## Foundation Week: Environment Setup and Tool Installation

This week focuses on preparing the development environment with essential open-source EDA tools for the complete RTL-to-GDSII flow.

### Tasks Overview

| Task   | Description            | Tools Installed | Status |
|--------|------------------------|-----------------|--------|
| Task 0 | Tools Installation     | ✅ Yosys, Iverilog, GTKWave, Ngspice, Magic, Docker, OpenLane | ✅ Done |

### Tools Installed in Week 0 - Task 0

#### Core RTL Design & Synthesis Tools

- **Yosys**: RTL Synthesis & Logic Optimization
- **Iverilog**: Verilog Simulation & Compilation
- **GTKWave**: Waveform Viewer & Analysis
- **Ngspice**: Analog & Mixed-Signal Simulation
- **Magic**: VLSI Layout Design & DRC Verification

# Week 0 — Task 0: EDA Tools Installation

This document provides step-by-step instructions for installing the open-source EDA tools needed for RTL-to-GDSII flows.

---

## 1️⃣ Yosys — RTL Synthesis

### Clone Yosys repository
git clone https://github.com/YosysHQ/yosys.git
cd yosys

### Install dependencies
sudo apt install make build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev

### Build and install Yosys
make
sudo make install

---

## Icarus Verilog - Verilog Simulation

### Install Icarus Verilog
sudo apt update
sudo apt install iverilog

## GTKWave — Waveform Viewer

### Install GTKWave
sudo apt update
sudo apt install gtkwave

