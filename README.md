# Horizon-Hv1.Ai
Compact dual-compute Edge AI development platform pairing a 1 TOPS-class neural accelerator with an ESP32-S3 MCU and unified memory on an advanced 6-layer high-speed PCB.


# HORIZON HV1.AI

> **Edge AI + Real-Time Embedded Computing Development Platform**
> A high-density, dual-compute development system integrating local neural acceleration (up to 1 TOPS-class), real-time control, unified high-throughput memory, and industrial expansion interfaces on an advanced 6-layer PCB.

---

## 📌 System Overview

HORIZON HV1.AI is an edge-native embedded computing platform engineered to bridge the gap between heavy deep learning inference and deterministic real-time hardware control. By coupling an on-chip AI acceleration engine with an ESP32-S3 microcontroller via a unified memory architecture, HV1.AI eliminates external computing modules, cloud latency, and memory interconnect bottlenecks.

```
+-----------------------------------------------------------------------------------+
|                                 HORIZON HV1.AI                                    |
|                                                                                   |
|   +--------------------------+                     +--------------------------+   |
|   |    AI COMPUTE ENGINE     |                     |    SYSTEM CONTROLLER     |   |
|   |  - Up to 1 TOPS Accel.   | <=================> |  - ESP32-S3 Dual-Core    |   |
|   |  - CNN / Vision Pipeline |   High-Speed Bus    |  - Real-Time RTOS        |   |
|   |  - Audio / Sensor ML     |                     |  - Wi-Fi 802.11 & BLE 5  |   |
|   +--------------------------+                     +--------------------------+   |
|                 │                                                │                |
|                 ▼                                                ▼                |
|   +---------------------------------------------------------------------------+   |
|   |                         UNIFIED MEMORY INTERFACE                          |   |
|   |  - Shared High-Bandwidth Frame Buffering & Weight Storage                 |   |
|   |  - High-Speed External Flash (GD25Q128-Class) + PSRAM Subsystem           |   |
|   +---------------------------------------------------------------------------+   |
|                 │                                                │                |
|                 ▼                                                ▼                |
|   +--------------------------+                     +--------------------------+   |
|   |     VISION & SENSORS     |                     |   INDUSTRIAL EXPANSION   |   |
|   |  - DVP / SPI Camera      |                     |  - CAN Controller / PHY  |   |
|   |  - IMU / ToF / I2C Hub   |                     |  - RS-485 / Modbus RTU   |   |
|   |  - High-Speed ADC/PWM    |                     |  - Isolated Digital I/O  |   |
|   +--------------------------+                     +--------------------------+   |
|                                                                                   |
|   +---------------------------------------------------------------------------+   |
|   |  USB-C Subsystem: Hardware Programming MUX (Auto-Switch AI / ESP32-S3)    |   |
|   +---------------------------------------------------------------------------+   |
+-----------------------------------------------------------------------------------+

```

---

## ⚙️ Technical Specifications

| Parameter | Specification | Details |
| --- | --- | --- |
| **AI Compute** | Neural Accelerator Engine | Up to 1 TOPS-class edge inference for CNN, YOLO, and vision tasks |
| **Host Controller** | ESP32-S3 Dual-Core Xtensa LX7 | 240 MHz, vector instructions, dedicated peripheral scheduler |
| **Wireless Connectivity** | 2.4 GHz Wi-Fi & Bluetooth 5 (LE) | Onboard antenna with dedicated RF impedance matching |
| **Memory Architecture** | Unified Memory Interface | High-speed shared Flash + PSRAM subsystem for frames and weights |
| **PCB Form Factor** | Advanced 6-Layer Stackup | Controlled impedance, dedicated ground/power planes, IPC Class 2/3 |
| **Development Interface** | Single USB Type-C | Integrated hardware multiplexer for selective target flashing and debug |
| **Vision Interface** | DVP / High-Speed SPI Camera | Direct memory DMA channel for low-latency image capture |
| **Industrial Bus Support** | CAN 2.0B, RS-485 (Transceiver Ready) | Compatible with Modbus RTU and distributed automation networks |
| **Power Management** | Multi-Rail LDO / Buck Regulators | Input protection, ESD suppressors, reverse-polarity defense |

---

## 🛠️ Hardware Engineering & Design Artifacts

### 1. 6-Layer PCB Stackup Architecture

To manage signal integrity for high-speed buses and prevent cross-talk between RF circuits and the AI accelerator, the board is designed on an advanced 6-layer stackup in **Altium Designer**:

* **Layer 1 (Top Signal):** High-speed differential pairs, RF routing, critical control lines.
* **Layer 2 (GND Plane):** Solid reference ground plane for impedance control and clean return paths.
* **Layer 3 (Inner Signal 1):** Low-speed peripheral buses (SPI, I2C, UART) and GPIO routing.
* **Layer 4 (Power Plane 1):** Split power planes (3.3V, 1.8V core, peripheral rails).
* **Layer 5 (GND Plane 2):** Secondary ground shield isolating power from bottom signal traces.
* **Layer 6 (Bottom Signal):** Power distribution traces, test points, secondary passives.

```
[ Layer 1 ]  ══════════════════  Top Signal / High-Speed Routing / RF
[ Layer 2 ]  ──────────────────  Solid Ground Plane (GND)
[ Layer 3 ]  ══════════════════  Inner Signal Routing (Buses / GPIO)
[ Layer 4 ]  ──────────────────  Power Distribution Plane (Split Rails)
[ Layer 5 ]  ──────────────────  Secondary Ground Plane (GND)
[ Layer 6 ]  ══════════════════  Bottom Signal / Secondary Components

```

### 2. Design Verification & Simulation Proofs

* **EDA Tool:** Altium Designer (Developed under the Altium 1-Year Academic License).
* **DFM / DRC:** Configured to stringent clearance, trace width, and annular ring limits per IPC standards.
* **SI/PI & Thermal Simulation:** Multi-rail power integrity and thermal dissipation verified via **Ansys Simulation** suites prior to fabrication sign-off.
* **Global Component Sourcing Matrix:**
* **United States:** Core microcontrollers, precision analog front-ends, power regulation ICs.
* **China:** Specialized accelerators, high-speed unified memory silicon, interconnect passives.
* **India:** Discrete passives, protection arrays, board-level mechanical hardware.



> **Design Verification Artifacts (Repository file paths):**
> * Schematic PDF: `docs/hardware/schematics_rev1.pdf`
> * 3D Interactive CAD Model: `docs/hardware/cad/horizon_hv1_ai_3d.step`
> * Ansys Thermal & Power Distribution Plots: `docs/simulation/ansys_power_thermal_report.pdf`
> * Layer Stackup & Impedance Profiles: `docs/hardware/stackup_impedance.xlsx`
> 
> 

---

## 💻 Software & Toolchain Ecosystem

```
             ┌──────────────────────────────────────────────┐
             │         Horizon HV1 Software Stack           │
             └──────────────────────┬───────────────────────┘
                                    │
       ┌────────────────────────────┼────────────────────────────┐
       ▼                            ▼                            ▼
┌───────────────┐          ┌───────────────────┐        ┌──────────────────┐
│  Horizon IDE  │          │    Custom RTOS    │        │  Horizon Web App │
│  & Mobile App │          │   & Device BSP    │        │  & Telemetry     │
└──────┬────────┘          └────────┬──────────┘        └────────┬─────────┘
       │                            │                            │
       ▼                            ▼                            ▼
  Model Converter              HAL Drivers                   Live Edge
  OTA Deployment            Dual-Core Sched.                 Diagnostics

```

* **Custom RTOS & Board Support Package (BSP):** Low-overhead real-time operating environment managing inter-processor communication (IPC) between the AI engine and the ESP32-S3 host.
* **Optimized Peripheral Drivers:** Custom-written C/C++ drivers for camera DMA pipelines, on-chip sensor arrays, and multiplexed USB communications. *(Scheduled for staged open-source release)*.
* **Horizon IDE (In Development):** Unified desktop workspace for training, quantization, model conversion, and one-click flashing.
* **Mobile Companion IDE & Web Dashboard:** Mobile configuration utility and full-stack web telemetry dashboard for remote system monitoring.

---

## 📊 Development Roadmap & Implementation Status

* [x] System Architecture Definition & Pinout Mapping
* [x] 6-Layer Schematic Capture & Library Management
* [x] Signal Integrity, Thermal, and Ansys Power Plane Simulations
* [x] IPC-Compliant DFM/DRC Verification
* [x] Global Component Procurement & Sourcing
* [x] Low-Level Peripheral Driver Architecture & Custom RTOS
* [ ] **Physical PCB Fabrication & SMT Assembly** *(Current Phase)*
* [ ] Hardware Bring-Up & Power Sequencing Validation
* [ ] Onboard Neural Inference & TOPS Verification Benchmarks
* [ ] Horizon Desktop IDE & Web Dashboard General Availability

---

## 👥 Engineering Team

| Contributor | Role & Core Responsibilities |
| --- | --- |
| **Dadasaheb P. Khaire** | **Project Lead** <br>

<br> • System Architecture & 6-Layer PCB Layout (IPC Standards) <br>

<br> • Custom RTOS Architecture & Inter-Process Communication <br>

<br> • Power Plane Routing, DFM/DRC Validation & Ansys Simulations <br>

<br> • Desktop Horizon IDE & OTA Pipeline Engineering |
| **Rohit Narkhede** | **Hardware & Mobile Systems Engineer** <br>

<br> • High-Speed Signal Routing & Differential Line Validation <br>

<br> • Schematic Verification & DRC Compliance Checks <br>

<br> • Companion Mobile IDE Development |
| **Mohit More** | **Firmware & Systems Integration Engineer** <br>

<br> • Component Sourcing, BOM Management & Schematic Library <br>

<br> • EMI/EMC Analysis & Hardware Simulation Support <br>

<br> • Custom Peripheral Driver Development & Web Dashboard Architecture <br>

<br> • 3D Product Rendering & CAD Animation |

---

## 📜 Acknowledgments & Licensing

* **Altium:** Special thanks to Altium for providing the 1-Year Student Software License, enabling high-speed multi-layer PCB design, impedance tuning, and professional rule-checking workflows.
* **Academic Development:** This project is actively designed, maintained, and brought up by undergraduate engineering students alongside full-time academic coursework.

---

```
Copyright (c) 2026 HORIZON Project Contributors.
Hardware design files and firmware drivers are licensed under the MIT License / CERN-OHL-P where applicable.

```
