## **Week 0 — Task 0: OpenLane Installation**

### **Objective**

Set up the **OpenLane** automated RTL-to-GDSII flow environment using Docker, ensuring a complete open-source VLSI design toolchain.

---

### **Steps for Installation**

1. **Install Docker**

   ```bash
   sudo apt update
   sudo apt install -y docker.io docker-compose
   sudo systemctl enable docker
   sudo systemctl start docker
   sudo usermod -aG docker $USER
   ```

   > Log out and log back in to apply Docker group changes.

2. **Clone OpenLane Repository**

   ```bash
   git clone https://github.com/The-OpenROAD-Project/OpenLane.git
   cd OpenLane
   ```

3. **Pull Docker Image**

   ```bash
   make mount
   ```

   This will pull the pre-built OpenLane Docker image with all dependencies.

4. **Verify Installation**

   ```bash
   ./flow.tcl -version
   ```

   > You should see OpenLane version details.

5. **Optional: Test Example Design**

   ```bash
   ./flow.tcl -design "tutorial" -overwrite
   ```

   This runs the OpenLane flow on a tutorial design to verify everything works.

---

### **Dependencies Installed**

* **Yosys**: RTL synthesis
* **Iverilog**: Verilog simulation
* **Magic**: Layout design & DRC
* **OpenROAD**: Automated physical design
* **Tech Files (sky130)**: Free PDK for tapeout

---

### **Key Notes**

* OpenLane is **Docker-based**, so your host OS doesn’t need heavy dependencies.
* Make sure your system has at least **16GB RAM** and **50GB free disk space** for smooth flow.
* Use `make clean` to remove previous build artifacts if you restart a design.


