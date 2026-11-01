# Sub-Volt TEG Energy Harvesting Boost Converter (BQ25504)

This repository contains the KiCad 8.0 hardware design, TINA-TI transient simulations, and project documentation for a sub-volt thermoelectric generator (TEG) energy harvesting boost converter. 

Designed around the Texas Instruments **BQ25504** ultra-low-power harvester, this circuit steps up 300mV–600mV DC inputs to a regulated 3.30V to intermittently power an ESP32-C3 telemetry load from a 10mF supercapacitor. While tested with a TEG, the sub-volt architecture is designed as an analog to evaluate power extraction from low-yield sources like Carbon-14 betavoltaic cells.

## ⚡ System Architecture & Specifications
* **Harvester IC:** Texas Instruments BQ25504 (330 nA quiescent current).
* **Cold-Start Voltage:** $\ge 330\text{ mV}$ (steps up from zero using an internal high-frequency oscillator and external $22\ \mu\text{H}$ inductor).
* **MPPT Network:** 50% Fractional Open-Circuit Voltage tracking for maximum power transfer, sampled every 16 seconds.
* **Storage Element:** 10 mF radial supercapacitor, providing 33.64 mJ of usable energy per discharge cycle.
* **Voltage Thresholds (Megaohm Dividers):**
  * Overvoltage Cutoff ($V_{\text{OV}}$): $\sim 3.30\text{ V}$ (protects the supercapacitor and load).
  * Undervoltage Cutoff ($V_{\text{UV}}$): $\sim 2.04\text{ V}.

## 🛠️ Hardware Design (sikhi_v1)
The 2-layer FR4 PCB measures 33.35 mm × 25.80 mm and was designed in KiCad 8.0 with strict analog layout rules:
* **Switching Node Isolation:** The noisy $22\ \mu\text{H}$ inductor switching loop is physically partitioned away from the high-impedance $10\text{ M}\Omega$ MPPT and threshold sensing dividers to prevent capacitive crosstalk.
* **Thermal Grounding:** The BQ25504 VQFN-16 exposed pad is stitched to an unbroken bottom ground plane using four $0.20\text{ mm}$ thermal vias for a low-impedance return path.
* **High-Frequency Bypassing:** A $100\text{ nF}$ low-ESL ceramic capacitor is placed immediately adjacent to the `VSTOR` pin to shunt MHz switching harmonics.
* **Assembly:** Designed for automated turnkey assembly (PCBA) using generated Pick & Place (CPL) and BOM files to prevent VQFN-16 package floating.

## 📂 Repository Contents
* `/Hardware/`: KiCad 8.0 schematic, PCB layout (`sikhi_v1`), and production-ready Gerber (.gbr) / Excellon drill (.drl) files.
* `/Simulation/`: TINA-TI transient SPICE models demonstrating the cold-start ramp, supercapacitor voltage coupling, and 64ms Nano-Power `VRDIV` sampling pulses.
* `/Docs/`: Final engineering report, component design calculations, layout verification, and manufacturing Bill of Materials.

## 👥 Project Team
**Pandit Deendayal Energy University (PDEU)**  
*Department of Electrical Engineering | Power Electronic Converters

* **Maharshi Dave** (24BEE010)
* **Vansh Soni** (24BEE027)
* **Yagna Khokhariya** (24BEE029)
* **Soham Trivedi** (24BEE059)

*Course Instructor & Evaluation: Prof. Het Bhalja*
