# Weight Budget — Open-Humanoid-180

This document provides an approximate weight breakdown of the robot's components.  
All weights are estimates based on manufacturer specifications, similar components, or reasonable assumptions.

**Target total weight:** ~45–50 kg.  
**Estimated total:** ~49–52 kg (depending on final material choices for reducers and structural parts).

---

## Motors

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| BLDC 6384 120KV | 6 | 0.65 | 3.90 | Typical weight for 6384 size outrunner. |
| BLDC 5065 140KV | 17 | 0.35 | 5.95 | Typical weight for 5065 size outrunner. |
| BLDC 3205 110KV | 13 | 0.15 | 1.95 | Lightweight gimbal motor. |
| **Motors subtotal** | | | **11.80** | |

---

## Motor Drivers

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| ODrive3.6 (clone) | 3 | 0.06 | 0.18 | PCB with heatsink. |
| Hoverboard mainboard (2-channel) | 9 | 0.10 | 0.90 | PCB with MOSFETs and caps. |
| SimpleFOCMini (MS8313) | 13 | 0.01 | 0.13 | Small driver board. |
| **Drivers subtotal** | | | **1.21** | |

---

## Sensors

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Magnetic encoder MT6826S | 36 | 0.002 | 0.07 | Small SMD module. |
| 9‑axis IMU BMI160 (with QMC5883L) | 11 | 0.002 | 0.02 | Module weight. |
| Pressure sensor FSR402 | 10 | 0.001 | 0.01 | Thin film sensor. |
| Load cell XNQJALYCY 100kg | 4 | 0.01 | 0.04 | Each with cable. |
| ADC HX711 | 4 | 0.002 | 0.01 | Small breakout board. |
| Dual HD USB Camera (OV4689) | 1 | 0.03 | 0.03 | With cable. |
| **Sensors subtotal** | | | **0.18** | |

---

## Compute & Logic

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Laptop RTX 2070 (stripped board) | 1 | 0.75 | 0.75 | Without case, screen, or battery. |
| ESP32‑S3 N16R8 | 1 | 0.01 | 0.01 | Small MCU board. |
| GPIO expansion board | 1 | 0.01 | 0.01 | Small PCB. |
| GD32F303 WeAct | 7 | 0.005 | 0.04 | Small MCU board. |
| TJA1050 (CAN transceiver) | 10 | 0.002 | 0.02 | Small module. |
| CD74HC4067 | 1 | 0.002 | 0.002 | Tiny chip. |
| **Compute subtotal** | | | **0.83** | |

---

## Battery & Power Regulation

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| LiFePO₄ 3.2V 50Ah (60145 cell) | 8 | 0.92 | 7.36 | 920g per cell (typical for 60145). |
| JK‑B2A8S20P Smart BMS (8S, 200A) | 1 | 0.20 | 0.20 | With heatsink and cables. |
| DC‑DC converter 1500W | 1 | 0.30 | 0.30 | Aluminum housing. |
| DC‑DC converter 600W | 1 | 0.15 | 0.15 | Aluminum housing. |
| DC‑DC converter 300W | 1 | 0.10 | 0.10 | Aluminum housing. |
| **Battery & power subtotal** | | | **8.11** | |

---

## Cables

| Cable                    | Length | Weight per meter (kg) | Total (kg) | Notes                  |
| :----------------------- | :----: | :-------------------: | :--------: | :--------------------- |
| KGTP‑HL 1×10 mm²         |  3 m   |         0.25          |    0.75    | Heavy copper.          |
| KGTP‑HL 2×4 mm²          |  12 m  |         0.15          |    1.80    | 2×4 mm² copper.        |
| KGTP‑HL 2×1.5 mm²        |  10 m  |         0.08          |    0.80    | Light power/signal.    |
| KGTP‑HL 2×0.75 mm²       |  5 m   |         0.05          |    0.25    | Thin power.            |
| KGTP‑HL 3×2.5 mm²        |  4 m   |         0.18          |    0.72    | Phase cables for 6384. |
| KGTP‑HL 3×1.5 mm²        |  10 m  |         0.10          |    1.00    | Phase cables for 5065. |
| KGTP‑HL 3×0.75 mm²       |  5 m   |         0.06          |    0.30    | Phase cables for 3205. |
| MKEShng(A)‑LS 5×0.35 mm² |  15 m  |         0.04          |    0.60    | Shielded signal.       |
| MKEShng(A)‑LS 2×0.35 mm² |  5 m   |         0.02          |    0.10    | Shielded signal.       |
| MGSHV 0.35 mm²           |  20 m  |         0.005         |    0.10    | Thin signal.           |
| **Cables subtotal**      |        |                       |  **6.42**  |                        |

---

## Connectors & Distribution

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Distribution block 160A | 2 | 0.15 | 0.30 | Metal block. |
| WAGO 221‑415 (5‑terminal) | 6 | 0.015 | 0.09 | Plastic terminal block. |
| WAGO 221‑413 (3‑terminal) | 2 | 0.01 | 0.02 | Plastic terminal block. |
| QS8P‑S (Anti‑Spark) | 1 pair | 0.05 | 0.05 | With resistor. |
| XT90 (pairs) | 6 | 0.02 | 0.12 | 6 pairs × 20g. |
| XT60 (pairs) | 12 | 0.01 | 0.12 | 12 pairs × 10g. |
| XT30 (pairs) | 5 | 0.005 | 0.025 | 5 pairs × 5g. |
| GX12 (5‑pin pairs) | 5 | 0.015 | 0.075 | Metal circular connector. |
| JST‑XH 2.54mm (set) | 1 | 0.02 | 0.02 | Plastic connectors. |
| **Connectors subtotal** | | | **0.82** | |

---

## Fuses & Protection

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| DC circuit breaker 200A | 1 | 0.30 | 0.30 | With bracket. |
| ATO fuse holder (10 slots) | 1 | 0.05 | 0.05 | Plastic housing. |
| ATO fuses (40A, 25A, 10A) | 10 | 0.002 | 0.02 | 10 pcs × 2g. |
| **Protection subtotal** | | | **0.37** | |

---

## Capacitors & Filtering

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Aluminium capacitor 50V 4700 µF | 6 | 0.015 | 0.09 | Large can. |
| Aluminium capacitor 25V 1000 µF | 10 | 0.005 | 0.05 | Medium can. |
| Ceramic capacitor 50V 0.1 µF | 100 | 0.0005 | 0.05 | Tiny SMD. |
| Resistor kit | 1 | 0.02 | 0.02 | Assorted. |
| **Filtering subtotal** | | | **0.21** | |

---

## Display

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Flexible LED P1.53 320×160mm | 1 | 0.20 | 0.20 | Flexible PCB with LEDs. |
| **Display subtotal** | | | **0.20** | |

---

## Structural Materials & Printing

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| PETG (10 kg filament) | — | — | 6.00 | Approx. 60% of filament ends up in parts. |
| TPU A95 (2 kg filament) | — | — | 1.00 | Approx. 50% used. |
| PA12‑CF (2 kg filament) | — | — | 1.00 | For reducers and cages. |
| 2‑part platinum silicone (10 kg) | — | — | 0.50 | Minimal applied (boots, damping). |
| Aluminium cast parts (reducers, brackets) | — | — | 3.00 | Estimated for 36 reducers. |
| Aluminum tubing (structural frame) | — | — | 3.00 | Skeleton. |
| **Structural subtotal** | | | **14.50** | |

---

## Fasteners & Hardware

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| TML 10‑6 lugs | 8 | 0.01 | 0.08 | Copper. |
| Ring terminals M6 | 9 | 0.005 | 0.045 | Copper. |
| Flanged nuts M6 | 16 | 0.005 | 0.08 | Steel. |
| Heatshrink, terminals, cable ties | 1 set | 0.20 | 0.20 | Various. |
| **Hardware subtotal** | | | **0.41** | |

---

## Reducers (36 pcs)

| Type | Qty | Material | Est. Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :--- | :---: | :---: | :--- |
| 1:100 (high‑torque) | 6 | Aluminium / PA12‑CF | 0.50 | 3.00 | Larger gears, more material. |
| 1:65 (medium) | 17 | Aluminium / PA12‑CF | 0.30 | 5.10 | Medium size. |
| 1:40 (base) | 13 | Aluminium / PA12‑CF | 0.20 | 2.60 | Smaller gears. |
| **Reducers subtotal** | | | | **10.70** | |

*Note: If printed in PA12‑CF instead of cast aluminium, weight will be ~30% lower.*

---

## Total Weight Summary

| Category | Weight (kg) |
| :--- | :---: |
| Motors | 11.80 |
| Motor Drivers | 1.21 |
| Sensors | 0.18 |
| Compute & Logic | 0.83 |
| Battery & Power Regulation | 8.11 |
| Cables | 6.42 |
| Connectors & Distribution | 0.82 |
| Fuses & Protection | 0.37 |
| Capacitors & Filtering | 0.21 |
| Display | 0.20 |
| Structural Materials | 14.50 |
| Fasteners & Hardware | 0.41 |
| Reducers (36 pcs) | 10.70 |
| **TOTAL** | **~55.76 kg** |

---

## Notes & Assumptions

- **Reducer weight** is the largest variable. Cast aluminium reducers are heavier; PA12‑CF printed reducers reduce weight significantly but may require thicker walls.
- **Cable weight** depends on actual routing lengths — this estimate assumes long runs typical for a 180 cm robot.
- **Structural frame** weight includes aluminum tubing for the skeleton and printed panels.
- **Battery cells** dominate the weight — 8× 920g = 7.36 kg. This is accurate for LiFePO₄ 60145 cells.
- **Laptop board** is stripped — no screen, keyboard, battery, or case.
- **Total weight** is expected to be **around 50 kg**, making the robot manageable for the selected actuators (6384 with 1:100 reducers have enough torque margin).

If weight reduction is needed, consider:
- Replacing aluminium reducers with PA12‑CF printed ones (saves ~3–4 kg).
- Using aluminum tubing with thinner walls (1–1.5mm).
- Shortening cable runs where possible.