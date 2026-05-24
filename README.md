# 180nm CMOS Inverter Physical Layout & Simulation

This repository contains the physical layout, SPICE netlist, and transient analysis for a standard CMOS inverter designed at the 180nm technology node. 

## 🛠 Toolchain
* **Schematic Verification:** LTspice
* **Physical Layout:** Magic VLSI
* **Extraction & Simulation:** Ngspice
* **Process Node:** 180nm Predictive Technology Model (PTM)

## 📐 Physical Design Specifications
The layout adheres to Scalable CMOS (SCMOS) design rules. To compensate for the lower mobility of holes compared to electrons, the PMOS transistor is sized at a 2:1 ratio relative to the NMOS to balance the pull-up and pull-down networks.
* **NMOS (W/L):** 4λ / 2λ 
* **PMOS (W/L):** 8λ / 2λ

## ⚡ Simulation & Performance Metrics
The layout was extracted to a SPICE netlist, capturing parasitic node capacitances ($C_{gd}$, $C_{gs}$, etc.). A transient analysis was performed using Ngspice to measure the precise propagation delay across the physical geometry.

**Measured Propagation Delay:**
* $t_{phl}$ (High-to-Low Delay): **1.37 ns**
* $t_{plh}$ (Low-to-High Delay): **2.24 ns**

*Note: The slight asymmetry in delay times reflects the physical reality of carrier mobility differences and extracted parasitic overlap capacitances at the 180nm scale.*

## 🪤 Design Traps Logged & Resolved
During the layout and simulation phase, several physical and simulation rule traps were identified and resolved. Maintaining this log prevents recurring silicon layout errors:
* **DRC Minimum Width Violation:** Initial polysilicon routing triggered a MOSIS #3.1 rule violation. Resolved by ensuring all poly wires maintained a strict minimum 2λ width.
* **PMOS Substrate Isolation:** Engine flagged missing N-Well. Resolved by drawing a surrounding N-Well to establish the necessary PN junction for the P-channel MOSFET.
* **SPICE Model Alignment:** Resolved a node mismatch where the extracted netlist names (`nfet`/`pfet`) did not match the PTM physics file headers, resulting in a dead pull-down network. Corrected the physics headers to align with the extraction engine.

## 🚀 How to Run
1. Clone the repository.
2. Ensure Ngspice is installed (`sudo apt install ngspice`).
3. Run the simulation: `ngspice first.spice`
