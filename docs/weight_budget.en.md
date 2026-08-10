# Weight Budget — Open-Humanoid-180

This document provides an approximate weight calculation of the robot by component categories.  
All weights are based on manufacturer specifications, data from similar components, or reasonable assumptions.

**Target weight:** ~45–50 kg.  
**Estimated weight:** ~53–55 kg (depends on reducer materials and structural parts).

---

## Motors

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| BLDC 6384 120KV | 6 | 0.65 | 3.90 | Typical weight for 6384. |
| BLDC 5065 140KV | 17 | 0.35 | 5.95 | Typical weight for 5065. |
| BLDC 3205 110KV | 13 | 0.15 | 1.95 | Light gimbal motor. |
| **Motors total** | | | **11.80** | |

---

## Motor Drivers

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| ODrive3.6 (clone) | 3 | 0.06 | 0.18 | Board with heatsink. |
| Hoverboard mainboard (2‑channel) | 9 | 0.10 | 0.90 | Board with MOSFETs and caps. |
| SimpleFOCMini (MS8313) | 13 | 0.01 | 0.13 | Small board. |
| **Drivers total** | | | **1.21** | |

---

## Sensors

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Magnetic encoder MT6826S | 36 | 0.002 | 0.07 | Small SMD module. |
| 9‑axis IMU BMI160 (with QMC5883L) | 11 | 0.002 | 0.02 | Module weight. |
| Pressure sensor FSR402 | 10 | 0.001 | 0.01 | Thin film. |
| Load cell XNQJALYCY 100kg | 4 | 0.01 | 0.04 | With cable. |
| ADC HX711 | 4 | 0.002 | 0.01 | Small board. |
| Dual HD USB Camera (OV4689) | 1 | 0.03 | 0.03 | With cable. |
| **Sensors total** | | | **0.18** | |

---

## Compute & Logic

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Laptop Lenovo L7 / R9 / RTX 3080 / 32GB / 1TB (bare board) | 1 | 0.85 | 0.85 | No case, screen, battery. |
| ESP32‑S3 N16R8 | 1 | 0.01 | 0.01 | MCU board. |
| GPIO expansion board | 1 | 0.01 | 0.01 | Small board. |
| AT32F403ACGU7 | 7 | 0.005 | 0.04 | MCU board. |
| TJA1042T (CAN transceiver) | 10 | 0.002 | 0.02 | Small module. |
| CD74HC4067 | 1 | 0.002 | 0.002 | Small IC. |
| **Logic total** | | | **0.93** | |

---

## Battery & Power Regulation

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Li‑NMC 3.7V 80.5Ah (pouch cell SK) | 7 | 0.90 | 6.30 | Actual cell weight ~900 g. |
| JK‑B2A8S20P BMS (8S, 200A) | 1 | 0.20 | 0.20 | With heatsink and wires. |
| Buck 1500W (28.8→19.5V) | 1 | 0.30 | 0.30 | Aluminium case. |
| Buck 600W (28.8→5V) | 1 | 0.15 | 0.15 | Aluminium case. |
| Buck 300W (28.8→5V) | 1 | 0.10 | 0.10 | Aluminium case. |
| **Battery & Power total** | | | **7.05** | |

---

## Cables

| Cable | Length | Weight per meter (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| KGTP‑HL 1×10 mm² | 3 m | 0.25 | 0.75 | Heavy copper. |
| KGTP‑HL 2×4 mm² | 12 m | 0.15 | 1.80 | 2×4 mm² copper. |
| KGTP‑HL 2×1.5 mm² | 10 m | 0.08 | 0.80 | Light power/signal. |
| KGTP‑HL 2×0.75 mm² | 5 m | 0.05 | 0.25 | Thin power. |
| KGTP‑HL 3×2.5 mm² | 4 m | 0.18 | 0.72 | Phase cables for 6384. |
| KGTP‑HL 3×1.5 mm² | 10 m | 0.10 | 1.00 | Phase cables for 5065. |
| KGTP‑HL 3×0.75 mm² | 5 m | 0.06 | 0.30 | Phase cables for 3205. |
| MKEShng(A)‑LS 5×0.35 mm² | 15 m | 0.04 | 0.60 | Shielded signal. |
| MKEShng(A)‑LS 2×0.35 mm² | 5 m | 0.02 | 0.10 | Shielded signal. |
| MGSHV 0.35 mm² | 20 m | 0.005 | 0.10 | Thin signal. |
| **Cables total** | | | **6.42** | |

---

## Connectors & Distribution

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Distribution block 250A (12 terminals) | 2 | 0.15 | 0.30 | Metal block. |
| WAGO 221‑415 (5‑terminal) | 6 | 0.015 | 0.09 | Plastic terminal. |
| WAGO 221‑413 (3‑terminal) | 2 | 0.01 | 0.02 | Plastic terminal. |
| QS8P‑S (Anti‑Spark) | 1 pair | 0.05 | 0.05 | With resistor. |
| XT90 (pairs) | 6 | 0.02 | 0.12 | 6 pairs × 20 g. |
| XT60 (pairs) | 12 | 0.01 | 0.12 | 12 pairs × 10 g. |
| XT30 (pairs) | 5 | 0.005 | 0.025 | 5 pairs × 5 g. |
| GX12 (5‑pin pairs) | 5 | 0.015 | 0.075 | Metal circular connector. |
| JST‑XH 2.54mm (set) | 1 | 0.02 | 0.02 | Plastic connectors. |
| **Connectors total** | | | **0.82** | |

---

## Fuses & Protection

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| DC breaker 200A | 1 | 0.30 | 0.30 | With mounting. |
| ATO fuse holder (10 slots) | 1 | 0.05 | 0.05 | Plastic housing. |
| ATO fuses (40A, 25A, 10A) | 10 | 0.002 | 0.02 | 10 pcs × 2 g. |
| Single holders with 80A fuses | 3 | 0.02 | 0.06 | For each ODrive. |
| **Protection total** | | | **0.43** | |

---

## Capacitors & Filtering

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Aluminium capacitor 50V 4700 µF | 6 | 0.015 | 0.09 | Large can. |
| Aluminium capacitor 25V 1000 µF | 10 | 0.005 | 0.05 | Medium can. |
| Ceramic capacitor 50V 0.1 µF | 100 | 0.0005 | 0.05 | Small SMD. |
| Resistor kit | 1 | 0.02 | 0.02 | Assorted. |
| **Filtering total** | | | **0.21** | |

---

## Display

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Flexible LED P1.53 320×160mm | 1 | 0.20 | 0.20 | Flexible PCB with LEDs. |
| **Display total** | | | **0.20** | |

---

## Structural Materials & Printing

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| PETG (10 kg filament) | — | — | 6.00 | About 60% of filament becomes parts. |
| TPU A95 (2 kg filament) | — | — | 1.00 | About 50% used. |
| PA12‑CF (2 kg filament) | — | — | 1.00 | For reducers and housings. |
| 2‑part silicone (10 kg) | — | — | 0.50 | Minimal use (feet, dampers). |
| Aluminium casting (reducers, brackets) | — | — | 3.00 | Estimated for 36 reducers. |
| Aluminium tubes (frame) | — | — | 3.00 | Skeleton. |
| **Structure total** | | | **14.50** | |

---

## Fasteners & Hardware

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| TML 10‑6 lugs | 8 | 0.01 | 0.08 | Copper. |
| Ring terminals M6 | 9 | 0.005 | 0.045 | Copper. |
| Flanged nuts M6 | 16 | 0.005 | 0.08 | Steel. |
| Heatshrink, terminals, cable ties | 1 set | 0.20 | 0.20 | Various. |
| **Fasteners total** | | | **0.41** | |

---

## Reducers (36 pcs)

| Type | Qty | Material | Est. unit weight (kg) | Total (kg) | Notes |
| :--- | :---: | :--- | :---: | :---: | :--- |
| 1:100 (high torque) | 6 | Aluminium / PA12‑CF | 0.50 | 3.00 | Larger, more material. |
| 1:65 (medium) | 17 | Aluminium / PA12‑CF | 0.30 | 5.10 | Medium size. |
| 1:40 (basic) | 13 | Aluminium / PA12‑CF | 0.20 | 2.60 | Smaller. |
| **Reducers total** | | | | **10.70** | |

*Note: Printing from PA12‑CF instead of aluminium casting will reduce weight by roughly 30%.*

---

## Summary Weight Table

| Category | Weight (kg) |
| :--- | :---: |
| Motors | 11.80 |
| Drivers | 1.21 |
| Sensors | 0.18 |
| Logic | 0.93 |
| Battery & Power | 7.05 |
| Cables | 6.42 |
| Connectors | 0.82 |
| Protection | 0.43 |
| Filtering | 0.21 |
| Display | 0.20 |
| Structure | 14.50 |
| Fasteners | 0.41 |
| Reducers (36 pcs) | 10.70 |
| **TOTAL** | **~54.86 kg** |

---

## Notes and Assumptions

- **Reducer weight** is the most variable. Aluminium is heavier; PA12‑CF printed ones are lighter but may require thicker walls.
- **Cable weight** depends on actual routing lengths — calculation is for typical lengths in a 180 cm robot.
- **Frame weight** includes aluminium tubes and printed panels.
- **Battery** (7S Li‑NMC 80.5Ah) weighs 6.3 kg (7 cells × 0.9 kg). This is the actual weight for the specified SK cells.
- **Laptop board** (RTX 3080) weighs about 0.85 kg without case and peripherals.
- **Final weight** is expected around **55 kg**, which is acceptable for the selected actuators (6384 with 1:100 reducers have sufficient torque margin).

To reduce weight, consider:
- Replacing aluminium reducers with PA12‑CF printed ones (save ~3–4 kg).
- Using aluminium tubes with thinner walls (1–1.5 mm).
- Shortening cable runs where possible.