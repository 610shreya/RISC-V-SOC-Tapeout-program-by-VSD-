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

# Day 0 - Tools Installation

## Yosys

```bash
# Clone Yosys
git clone https://github.com/YosysHQ/yosys.git
cd yosys

# Install dependencies
sudo apt install make build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev

##i-verilog

# Build and install
make
sudo make install

sudo apt update
sudo apt install iverilog

##GTKWave
sudo apt update
sudo apt install gtkwave

##Magic VLSI

# Install dependencies
sudo apt-get install m4 tcsh csh libx11-dev tcl-dev tk-dev \
    libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev \
    libxpm-dev

# Clone Magic
git clone https://github.com/RTimothyEdwards/magic.git
cd magic

# Build and install
./configure
make
sudo make install

#### Advanced Flow Tools

- **Docker**: Containerization Platform
- **OpenLane**: Complete RTL-to-GDSII Flow

### Key Learnings from Week 0

- Successfully installed and verified open-source EDA tools ecosystem
- Mastered environment setup for professional RTL design and synthesis workflows
- Prepared comprehensive system for upcoming RTL → GDSII flow experiments
- Established Docker-based OpenLane environment for automated design flows
- Configured virtual machine with optimal specifications for EDA workloads

###✅ Summary
At the end of Day 0, the following tools should be working on your system:
Yosys – RTL synthesis
Icarus Verilog – Verilog simulation
GTKWave – Waveform viewer
Ngspice – Circuit simulation
Magic – Layout & DRC verification
OpenLane – Complete RTL-to-GDSII flow 
