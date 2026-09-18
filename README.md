# Hardware Incident Post-Mortem: RAM Diagnostics & Isolation

## Incident Overview
This document details the hardware diagnostic methodology, hardware isolation process, and final resolution for a physical memory failure encountered on my primary desktop workstation (`JOSH-DESKTOP`)[cite: 1].

* **Host System:** Gigabyte Z390 AORUS PRO WIFI-CF / Intel Core i7-8700K[cite: 1]
* **Affected Component:** Physical RAM Module
* **Diagnostic Indicator:** Motherboard Debug POST LED (`DRAM`)
* **Status:** Resolved / Defective Module Isolated & Replaced

---

## Technical Symptoms & Initial Detection
* System failed to complete the Power-On Self-Test (POST) cycle and would not boot into the OS.
* **Hardware Alert:** The built-in motherboard **DRAM status LED** illuminated solid during the boot sequence, indicating a memory initialization failure prior to video signal output.
* Intermittent system crashes and memory address exceptions occurred under heavy workloads prior to total boot failure.

---

## Step-by-Step Diagnostic Methodology

1. **CMOS Reset & Baseline:**
   * Cleared motherboard CMOS to reset memory frequencies, XMP profiles, and timings to default JEDEC baselines, ruling out overclocking instability.

2. **Hardware Isolation (Single-Stick Elimination):**
   * Powered down system, disconnected AC power, and unseated all RAM modules from the motherboard slots.
   * Installed a single RAM stick into the primary recommended slot and attempted a system boot.
   * Repeated this isolation process sequentially—testing each module individually, one at a time—while monitoring the motherboard POST LEDs.

3. **Fault Identification:**
   * **Result:** The system successfully cleared POST and booted with specific modules, but consistently halted on the `DRAM` status LED when one specific stick was seated.
   * Isolated the single defective memory module causing the system-wide memory bus error.

---

## Final Resolution & Verification

* **Corrective Action:** Removed the defective RAM module from the system and populated the remaining functional modules back into designated dual-channel memory slots.
* **System Initialization:** Flashed motherboard BIOS to revision F14a to maintain maximum stability and memory controller compatibility[cite: 1].
* **Verification:** Successfully booted into Windows 11 Home and confirmed stable, error-free operation across extended stress testing, with full active physical memory correctly addressed in System Information (`msinfo32`)[cite: 1].
