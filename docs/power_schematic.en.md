# Power Distribution Schematic — Open-Humanoid-180

This document describes the complete power distribution architecture of the robot — from the battery to each actuator, compute module, and sensor.

---

## System Overview

- **Battery:** 8S LiFePO₄ (Liitokala 60145, 50Ah) — nominal 25.6V, max 28.8V (29.2V at 3.65V per cell).
- **BMS:** JK-B2A8S20P (200A continuous, 8S).
- **Main protection:** 200A DC circuit breaker.
- **Distribution:** Two 160A distribution blocks (positive and negative rails) with 8 outputs each.
- **Secondary protection:** 10‑slot ATO fuse hub for individual load lines.
- **Voltage rails:** 28.8V (motors, direct), 19.5V (laptop), 5V (logic & display), 6V/12V (optional).

---

## Battery Pack Assembly

### Cells
- 8 cells of LiFePO₄ 3.2V 50Ah (60145) connected in **8S1P** configuration.
- **Inter‑cell connections:** M6 copper busbars (included with cells) — used strictly for short links between cell blocks.

### Inter‑block Jumpers
- **Cable:** KGTP‑HL 1×10 mm² — cut into short jumpers between separated cell blocks.
- **Connectors:** XT90 pairs soldered to the ends (Male on one block output, Female on the next block input).
- **Current:** Walking mode draw < 30A; 3× safety margin on XT90 ensures no heating.

### Battery Wiring to BMS & Breaker
- **Positive:** From battery (+) → KGTP‑HL 1×10 → **200A DC breaker** → 160A distribution block (+).
- **Negative:** From battery (–) → KGTP‑HL 1×10 → BMS (–) → 160A distribution block (–).
- **Cable length:** 3 meters total.

### Balance Wiring
- **Cable:** MGSHV 0.35 mm² — 20 meters.
- **Connections:** Crimped with ring terminals M6 and stacked on top of busbars.
- **Function:** Balance leads from JK BMS to each cell block.

### Fasteners & Insulation
- **Flanged M6 nuts with serrations (DIN 6923):** 16 pcs — replace standard nuts to prevent loosening from vibration.
- **Ring terminals M6 (insulated):** 9 pcs.
- **Heat‑shrink tubing 12mm (adhesive-lined):** 1 meter — insulates TML lug crimp points.

---

## Main Power Bus (28.8V)

### Primary Distribution
After the 200A breaker, power goes to:
- **Positive block:** 160A distribution block (6 outputs used).
- **Negative block:** 160A distribution block (6 outputs used).

### Fuse Hub (10‑slot ATO)
5 cables of **KGTP‑HL 2×4 mm²** (12 meters total) connect the positive distribution block to the fuse hub inputs:

- Each cable uses **both cores** paralleled (≈8 mm² equivalent) on the distribution side, crimped into one NSHVI ferrule.
- On the hub side, cores are split back into two independent 4 mm² wires, terminated with 6.3mm female terminals.
- **5 cables × 2 wires = 10 inputs** — fully populates the hub.

### Load Lines from Fuse Hub (10 lines)

| Line | Load | Fuse | Cable from Hub to Load | Notes |
| :--- | :--- | :---: | :--- | :--- |
| 1 | 1500W buck converter → laptop (19.5V) | 25A | KGTP‑HL 2×1.5 | Powers RTX 2070 laptop board. |
| 2 | 600W buck converter → LED face (5V) | 25A | KGTP‑HL 2×1.5 | Powers flexible LED P1.53 display. |
| 3 | 300W buck converter → logic (5V) | 25A | KGTP‑HL 2×0.75 | ESP32-S3, 11× BMI160, 7× GD32F303. |
| 4 | Left leg — 2× ODrive3.6 (6384) | 40A | KGTP‑HL 2×4 | High-torque knee & hip motors. |
| 5 | Right leg — 2× ODrive3.6 (6384) | 40A | KGTP‑HL 2×4 | High-torque knee & hip motors. |
| 6 | Waist — 1× ODrive3.6 (6384) + 1× hoverboard ESC | 40A | KGTP‑HL 2×4 | Torso bending & rotation. |
| 7 | Left arm — WAGO 5‑terminal (×2) | 40A | KGTP‑HL 2×4 | Powers hoverboard ESCs + SimpleFOCMini for fingers. |
| 8 | Right arm — WAGO 5‑terminal (×2) | 40A | KGTP‑HL 2×4 | Powers hoverboard ESCs + SimpleFOCMini for fingers. |
| 9 | Torso/abdomen — WAGO 3‑terminal (×2) | 40A | KGTP‑HL 2×4 | Powers 2× hoverboard ESCs (5065 motors). |
| 10 | Head/neck — WAGO 3‑terminal | 10A | KGTP‑HL 2×1.5 | Neck drivers and sensors. |

---

## Secondary Load Wiring (After WAGO Terminals)

### Cable KGTP‑HL 2×1.5 (10 meters)
- From WAGO terminals (5‑terminal blocks, using 3 of 5 contacts) to:
  - Hoverboard ESC boards.
  - Buck converters (input side).
- From buck converters to loads:
  - **19.5V (1500W buck) → laptop** (power input).
  - **5V (600W buck) → LED display** and other high‑current 5V loads.
  - **WAGO (5‑terminal, 1 of 5) → SimpleFOCMini** drivers for fingers.

### Cable KGTP‑HL 2×0.75 (5 meters)
- From 5V 300W buck converter → all low‑current logic:
  - ESP32-S3.
  - 7× GD32F303 boards.
  - 11× BMI160+QMC5883L IMUs.
  - Other sensors.

### Cable MKEShng(A)-LS 5×0.35 (15 meters)
- Shielded signal cable.
- Used between all distributed controllers, sensors, and encoders.
- Carries SPI (MT6826S), UART (ESC bridge), and CAN (TJA1050) signals.
- Single‑point grounding of shield to the negative distribution block to avoid ground loops.

---

## Motor Phase Wiring

| Motor Type | Cable | Length | From → To |
| :--- | :--- | :---: | :--- |
| 6384 120KV (6 pcs) | KGTP‑HL 3×2.5 | 4 m | Leg hoverboard ESCs → 6384 motors |
| 5065 140KV (17 pcs) | KGTP‑HL 3×1.5 | 10 m | Hoverboard ESCs (torso/arms) → 5065 motors |
| 3205 110KV (13 pcs) | KGTP‑HL 3×0.75 | 5 m | SimpleFOCMini → 3205 motors |

---

## Capacitors & Filtering

### Main Bus Buffer (Torso)
- **2× Aluminium 50V 4700 µF** — connected directly between the positive and negative 160A distribution blocks.
- Absorbs regenerative braking spikes from 6384 motors.

### Buck Converter Output Filters
- **3× Aluminium 25V 1000 µF** — one per converter output:
  - 19.5V (laptop rail)
  - 5V 600W (display rail)
  - 5V 300W (logic rail)

### Local Driver Protection (Arms & Neck)
- **3× Aluminium 50V 1000/4700 µF** — placed on WAGO terminals inside arms and neck (28.8V input).

### High‑Frequency Decoupling
- **Ceramic 50V 0.1 µF (code 104)** — soldered directly on power pins of:
  - Every SimpleFOCMini driver.
  - Every MT6826S encoder.
  - Every BMI160 IMU.
- Suppresses PWM noise from motor drivers.

---

## Connectors & Distribution Components

| Component | Qty | Function |
| :--- | :---: | :--- |
| **160A distribution block** | 2 | Positive and negative main rails. |
| **WAGO 221‑415 (5‑terminal)** | 6 | Power distribution in arms (×2) and neck/head. |
| **WAGO 221‑413 (3‑terminal)** | 2 | Torso/abdomen power distribution. |
| **QS8P‑S (Anti‑Spark)** | 1 pair | Main power input connector. Installed between BMS output and the 200A breaker. Prevents sparking when connecting the battery. |
| **XT90 (pairs)** | 6 pairs | Quick‑disconnect for leg and ODrive lines (28.8V, high current). Female side on fuse hub outputs, Male side on load cables. |
| **XT60 / XT60h (pairs)** | 12 pairs | Medium‑power connections: laptop buck input, 5V buck inputs, arm hoverboard ESCs. XT60h used for shoulder joints (with caps). |
| **XT30 (pairs)** | 5 pairs | Low‑power 28.8V connections: SimpleFOCMini power in forearms, neck drivers, and micro‑buck for fans. |
| **GX12 (5‑pin, pairs)** | 5 pairs | Signal connectors for shielded MKESH cables. Installed at limb joints (shoulders, hips, neck). Shield connected to connector body for continuous EMI protection. |
| **JST‑XH 2.54mm (set)** | 1 set | Local sensor connectors inside limbs: 4‑pin for BMI160 (I2C), 5/6‑pin for MT6826S (SPI). Plugs directly into GD32F303 and ESP32‑S3 pin headers. |

---

## Protection Summary

| Protection Device | Qty | Location | Rating |
| :--- | :---: | :--- | :--- |
| DC breaker | 1 | Main positive line (after QS8P, before distribution) | 200A |
| ATO fuse holder | 1 | After positive distribution block | 10 slots |
| ATO fuse 40A | 7 | Legs (×2), waist, arms (×2), torso | 40A |
| ATO fuse 25A | 2 | Laptop buck, 5V 600W buck, 5V 300W buck | 25A |
| ATO fuse 10A | 1 | Head/neck | 10A |

---

## Cable Summary

| Cable                | Length |
| :------------------- | :----: |
| KGTP‑HL 1×10         |  3 m   |
| KGTP‑HL 2×4          |  12 m  |
| KGTP‑HL 2×1.5        |  10 m  |
| KGTP‑HL 2×0.75       |  5 m   |
| KGTP‑HL 3×2.5        |  4 m   |
| KGTP‑HL 3×1.5        |  10 m  |
| KGTP‑HL 3×0.75       |  5 m   |
| MKEShng(A)‑LS 5×0.35 |  15 m  |
| MKEShng(A)‑LS 2×0.35 |  5 m   |
| MGSHV 0.35           |  20 m  |
