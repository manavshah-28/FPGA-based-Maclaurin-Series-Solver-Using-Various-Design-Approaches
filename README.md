# 💻 Maclaurin Series Solver on FPGA — High Performance & Area-Efficient Design

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Platform: Quartus](https://img.shields.io/badge/Platform-Intel%20Quartus%20Prime-blue.svg)]()
[![FPGA: DE1-SoC](https://img.shields.io/badge/Board-DE1--SoC-green.svg)]()

## 🧠 Overview

This repository showcases a series of three FPGA-based digital design projects focused on solving the Maclaurin Series expansion of \( e^x - 1 \) using softcore processors and hardware-optimized arithmetic modules. Each project explores different design objectives—**functional correctness**, **performance optimization**, and **area minimization**—implemented on the Intel DE1-SoC development board.

This project was done in compliance of the Digital Design 2 course ECE 4514 at Virginia Tech.
---

## 📂 Projects Summary

### 📘 Project 1: **Maclaurin Series Solver using Softcore Processor**

- **Objective**: Compute the first 4 terms of the Maclaurin series for \( e^x - 1 \) using a NIOS II softcore processor.
- **Methodology**:
  - Custom bare-metal C implementation running on a NIOS II softcore.
  - Integrated with Quartus Platform Designer.
  - Approximated \( e^x - 1 \approx x + x^2/2 + x^3/6 + x^4/24 \)
- **Optimizations**:
  - Removed unnecessary print/debug statements.
  - Direct computation without using `<math.h>` and `pow()`.
  - Final implementation achieved **70,918 cycles** (from 2.5M+ initially).
- **Area**: `1883.168` units  
- **Visual Output**: Results displayed on HEX displays with input toggled via switches.

📄 [Read Full Report »](reports/Project1_ManavShah.pdf)

---

### ⚙️ Project 2: **High-Performance Maclaurin Series Solver**

- **Objective**: Improve performance using custom-designed hardware arithmetic modules.
- **Optimizations**:
  - Rewrote equation as:  
    \( e^x - 1 = \frac{x}{24}(24 + 12x + 4x^2 + x^3) \)
  - Replaced all division operations with multiplications.
  - Introduced low-latency arithmetic IPs (5-cycle multipliers and adders).
  - Added delay modules to equalize critical paths and support pipelining.
- **Design Highlights**:
  - Custom Delay Modules using Flip-Flops.
  - Carefully balanced latency pipeline.
- **Area**: `1970` units  
- **Max Operating Frequency**: Derived from Quartus analysis tools.

📄 [Read Full Report »](reports/Project2_ManavShah.pdf)

---

### 📉 Project 3: **Area-Optimized Maclaurin Series Solver**

- **Objective**: Minimize FPGA resource usage while maintaining functional correctness.
- **Methodology**:
  - **Single Adder & Multiplier** reused across multiple steps.
  - Controlled using a **Finite State Machine (FSM)** and multiplexers.
  - Stored intermediate results in registers.
- **Performance**:
  - Fixed 20-cycle latency for each computation.
  - Operated at **91.77 MHz**, yielding 218 ns total computation time.
- **Area**: **Only `592` units**, a significant reduction.
- **Validation**: All output waveforms and hex results matched expected Maclaurin outputs.

📄 [Read Full Report »](reports/Project3_ManavShah.pdf)

---

## 🔬 Technical Stack

- **Platform**: Intel DE1-SoC (Cyclone V)
- **Software**:
  - Intel Quartus Prime
  - Platform Designer
  - NIOS II SBT for Eclipse
- **Languages**:
  - SystemVerilog (Testbenches, FSMs)
  - C (Bare-metal Programming)
  - VHDL/Verilog (Quartus RTL)

---

## 🧪 Sample Results

| Input `x` | Expected Output | Solver Output (Hex) | Result (Float) |
|-----------|------------------|----------------------|----------------|
| -0.3      | -0.2591625       | `be84b0f2`           | -0.25916252    |
|  0        | 0.0              | `0`                  | 0.0            |
|  0.3      | 0.3498375        | `3eb31de8`           | 0.34983775     |
|  1.0      | 1.7083333        | `3fdaaaaa`           | 1.7083334      |

---

## 📌 Key Learnings

- Trade-offs between **speed**, **area**, and **resource usage** are critical in embedded system design.
- FSM-based reuse of arithmetic IPs allows significant savings in logic usage.
- Hardware-oriented rewrites of mathematical expressions lead to better synthesis outcomes.
- Bare-metal programming ensures tight control over cycle counts.

---

## 👨‍💻 Author

**Manav Bhavesh Shah**  
M.S. Student, Bradley Department of Electrical and Computer Engineering  
Virginia Polytechnic Institute and State University  
📧 manavbs28@vt.edu

---