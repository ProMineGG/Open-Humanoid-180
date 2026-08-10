# Open-Humanoid-180
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![GitHub stars](https://img.shields.io/github/stars/ProMineGG/Open-Humanoid-180)](https://github.com/ProMineGG/Open-Humanoid-180/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/ProMineGG/Open-Humanoid-180)](https://github.com/ProMineGG/Open-Humanoid-180/issues)
[![GitHub last commit](https://img.shields.io/github/last-commit/ProMineGG/Open-Humanoid-180)](https://github.com/ProMineGG/Open-Humanoid-180/commits)

[Roadmap](https://github.com/ProMineGG/Open-Humanoid-180/issues/1)

*Read this in other languages: [Русский](README.md)*

**A 180 cm DIY bipedal humanoid robot — built with off‑the‑shelf parts, custom wave reducers with rolling elements, and a distributed control network.**

---

## Overview

This project is a full‑size (180 cm, ~55 kg) walking robot with onboard vision‑language AI, with a target BOM under $3,500.  
Instead of expensive industrial actuators, the design uses:

- **Two‑stage wave reducers with intermediate rolling elements (ПТК)** – standard steel bearing rollers as rolling bodies. For high‑torque joints (6384) the overall ratio 1:100 is achieved by two 1:10 stages; for medium (5065) and base (3205) joints, dedicated two‑stage setups give overall ratios 1:65 and 1:40.
- **BLDC outrunners** (6384, 5065, 3205) – 36 degrees of freedom total.
- A **stripped gaming laptop (RTX 3080)** as the main AI brain (an affordable alternative to expensive specialised modules, offering better performance for the price).
- A **distributed control network** – ESP32‑S3 as CAN gateway, AT32F403ACGU7 (GD32F303‑compatible) for low‑level FOC, and hacked hoverboard ESCs for medium motors.

Mechanical parts are designed for **backyard aluminium casting** (coal‑fired furnace) or 3D printing (PETG / PA12‑CF) on an Ender 3 V3 Plus.

---

## Key Specifications

| Parameter              | Value                                                         |
| :--------------------- | :------------------------------------------------------------ |
| Height / Target Weight | 180 cm / ~55 kg                                               |
| Degrees of Freedom     | 36 (6 High‑torque, 17 Medium, 13 Base)                        |
| Battery                | 7S Li‑NMC (SK 3.7V 80.5Ah) + JK Smart BMS (200A peak)         |
| Main Power Bus         | 25.9–29.4 V (nominal 25.9 V, max 29.4 V)                      |
| Secondary Rails        | 19.5 V (laptop), 5 V (logic & display), 6 V / 12 V (future)   |
| Compute                | Laptop Lenovo L7 / R9 / RTX 3080 / 32GB / 1TB (Ubuntu 22.04 + RT‑Preempt) |
| Real‑time Node         | ESP32‑S3 (CAN gateway, IMU fusion, I/O expansion)             |
| Motor Controllers      | ODrive3.6 (x3), Hoverboard ESCs (x9), SimpleFOCMini (x13)     |
| Communication          | CAN (TJA1042T) + SPI (encoders) + UART (ESC bridge)           |
| Sensors                | 11× BMI160+QMC5883L, 10× FSR402, 4× XNQJALYCY 100kg load cells |
| License                | **GNU GPLv3** (code, CAD, schematics)                         |

---

## Actuator Layout & Reducers

The mechanical design is modular:

- **Legs (8 actuators):**  
  – 6× 6384 120KV (1:100) – knees and hip sagittal axes  
  – 2× 5065 140KV (1:65) – hip rotation

- **Torso & Neck (6 actuators):**  
  – 3× 5065 140KV (1:65) – torso bending / rotation  
  – 3× 3205 110KV (1:40) – neck (2 bending + 1 rotation)

- **Arms (22 actuators):**  
  – 6× 5065 (shoulders: 2 bending + 1 rotation per side)  
  – 2× 5065 (elbows)  
  – 4× 5065 (wrists – 2 per arm, placed in forearms with Bowden cables)  
  – 10× 3205 110KV (fingers – 5 per hand, 1:40)

- **Reducers:**  
  Custom **wave gears with rolling elements (ПТК)**.  
  – All joints use a **two‑stage design**; overall ratios: 1:100 (high‑torque), 1:65 (medium), 1:40 (base).  
  – Rolling elements are standard steel bearing rollers (cheap, wear‑resistant).  
  – Housings are cast in aluminium or printed in PA12‑CF.

---

## Power Distribution & Protection

- **Battery:** 7S Li‑NMC (SK 3.7V 80.5Ah, pouch cells) – high energy density at moderate weight.  
- **BMS:** JK‑B2A8S20P (200A continuous, supports 7S) with Bluetooth monitoring.  
- **Main protection:** 200A DC circuit breaker on the positive line.  
- **Fuse hub:** 10‑slot ATO fuse block – 40A for arms/torso, 25A for laptop and 5V converters, 10A for head peripherals.  
- **Separate ODrive fuses:** 3 single holders with 80A fuses – one per ODrive3.6, fed directly from the distribution blocks (not through the ATO hub).  
- **Distribution blocks:** two 250A (12‑terminal) blocks – positive and negative bus bars.  
- **Bus capacitors:** 2× 4700 µF / 50V – absorb regenerative spikes.  
- **Local decoupling:** 0.1 µF ceramics on every SPI/I2C device and driver board to suppress PWM noise.  
- **Wiring:** shielded MKESH cables for all signal lines (single‑point grounded to the negative distribution block) to avoid ground loops.

All DC‑DC converters (1500W, 600W, 300W) are **over‑specified** and run **passively cooled** – no extra fans except for the laptop’s 140 mm blower.

---

## Compute & Communication Architecture

### Layers

1. **High‑level (laptop)**  
   Runs Ubuntu 22.04 with Linux RT‑Preempt kernel. Hosts ROS2, YOLO, and VLM models (Qwen 3.5 9B / RT‑2X). Receives sensor data from ESP32 and sends high‑level movement commands.

2. **Mid‑level (ESP32‑S3)**  
   Polls 11× BMI160+QMC5883L (via SPI), 4× HX711 load‑cell ADCs, and the FSR402 array (via CD74HC4067 mux). Fuses IMU data into orientation estimates, then forwards them to the laptop. Also acts as the **CAN gateway** for all motor controllers.

3. **Low‑level (joint controllers)**  
   – **ODrive3.6** (x3) – runs FOC for the 6 high‑torque motors (6384) over CAN.  
   – **Hoverboard ESCs** (x9) – each drives 2 medium motors (5065). Total 18 channels, but only 17 are used (one spare). They only have **UART**, so we use **AT32F403ACGU7** (GD32F303‑compatible) as UART‑to‑CAN bridges: one MCU polls 2–3 ESCs and relays data to ESP32 via CAN.  
   – **SimpleFOCMini** (x13) – drives the 13 base motors (3205) directly from AT32F403ACGU7 boards (which also handle the SPI encoders).  
   – **Encoders:** 36× MT6826S magnetic sensors – 14‑bit absolute, SPI interface.

### Sensor Network

- **IMU nodes:** 11× BMI160 (accelerometer+gyro) each with an onboard QMC5883L magnetometer – routed in SPI mode to the ESP32 (I2C only used locally between BMI and QMC on the same module).  
- **Tactile:** 10× FSR402 in fingers → CD74HC4067 analog mux → ESP32 ADC.  
- **Foot force:** 4× XNQJALYCY 100kg load cells (2 per foot) → HX711 ADC → ESP32.

---

## Project Status (March 2026)

- [x] Full component selection and cost estimation (see `/docs/BOM.en.md`).
- [x] Preliminary power distribution and wiring scheme.
- [x] Aluminium casting test – successful (melting scrap in coal forge with salt degassing).
- [ ] 3D printer (Ender 3 V3 Plus) and materials ready.
- [ ] CAD models for all joint reducers (in progress – hand sketches available in `/assets`).
- [ ] First single‑joint prototype (active CAD development, tolerance analysis, and supplier sourcing; procurement will start after 3D modelling is complete).
- [ ] Firmware for ESP32 and AT32F403ACGU7 (will be published once tested).
- [ ] URDF model for Gazebo simulation.

---

## Repository Structure

* [`docs/BOM.en.md`](docs/BOM.en.md) – Full Bill of Materials with current prices, quantities, and direct links to Ozon / AliExpress / Avito.
* [`docs/power_schematic.en.md`](docs/power_schematic.en.md) – Power distribution diagram, fuse allocation (200A breaker, ATO hub, separate 80A for ODrive), and WAGO terminal block wiring.
* [`docs/weight_budget.en.md`](docs/weight_budget.en.md) – Mass breakdown per joint, total CoM estimation, and structural material selection (aluminium / PETG / PA12‑CF).

* [`docs/in progress/motor_selection.en.md`](docs/in%20progress/motor_selection.en.md) – Actuator calculations: KV selection, torque estimates per joint, and reduction ratio justification *(work in progress)*.
* [`docs/in progress/reducer_design.en.md`](docs/in%20progress/reducer_design.en.md) – Engineering details for the two-stage wave reducer with rolling elements (ПТК): cam profiles, roller sizing, bearing selection, and assembly tolerances *(work in progress)*.
* [`docs/in progress/casting_aluminium.en.md`](docs/in%20progress/casting_aluminium.en.md) – Step-by-step guide for backyard aluminium casting: furnace setup, degassing (salt + soda), sand moulds, and finishing on a lathe *(work in progress)*.
* [`docs/in progress/assembly_guide.en.md`](docs/in%20progress/assembly_guide.en.md) – Mechanical assembly sequence, wiring harness routing, MKESH shielding rules, and single‑point grounding instructions *(work in progress)*.
* [`docs/in progress/alternative_parts.en.md`](docs/in%20progress/alternative_parts.en.md) – Budget-friendly substitutes, ESC modding notes (hoverboard firmware hack), and fallback components *(work in progress)*.

* [`hardware/STL/`](./hardware/STL/) – 3D-printable files (PETG for housings, PA12‑CF for reducer cages, TPU for foot soles).
* [`hardware/CAD/`](./hardware/CAD/) – Source CAD models (FreeCAD / STEP format) – work in progress.
* [`software/esp32_firmware/`](./software/esp32_firmware/) – ESP32‑S3 code: IMU polling (SPI), CAN gateway, UART‑to‑CAN bridge logic.
* [`software/at32_firmware/`](./software/at32_firmware/) – AT32F403ACGU7 firmware: SimpleFOCMini driver, MT6826S encoder reading (SPI), and ESC UART communication.
* [`simulation/urdf/`](./simulation/urdf/) – URDF/XACRO model for Gazebo / Isaac Sim (to be added).

---

## Contributions & License

We welcome contributors with experience in:

- **ROS2 control** and **URDF/XACRO** modelling.
- **Low‑level FOC tuning** (especially current limits for low‑inductance BLDCs).
- **Simulation** (Gazebo / Isaac Sim) for walking gait development.
- **Mechanical CAD** (FreeCAD, Fusion 360) – we need help turning sketches into production‑ready models.

Detailed contribution guidelines are available in [CONTRIBUTING.en.md](CONTRIBUTING.en.md).

Feel free to open issues or pull requests. For discussions, a Telegram channel will be created soon.

**License:** All code, CAD, and schematics are released under the **GNU GPLv3**. Commercial use is permitted only if derivative work remains fully open‑source.

---

*Built with standard workshop tools, litres of technical coffee, and a stubborn refusal to buy overpriced proprietary parts.*