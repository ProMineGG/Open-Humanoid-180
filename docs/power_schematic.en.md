# Power Distribution Schematic — Open-Humanoid-180

This document describes the complete power distribution architecture of the robot — from the battery to each actuator, compute module, and sensor.

---

## Overall Structure

- **Battery:** 7S Li‑NMC (SK 3.7V 80.5Ah, pouch cells) — nominal 25.9V, max 29.4V (at 4.2V per cell).
- **BMS:** JK‑B2A8S20P (200A continuous, supports 7S, one channel unused).
- **Primary protection:** DC circuit breaker 200A.
- **Distribution:** two 250A distribution blocks (12 terminals each) — positive and negative bus bars.
- **Secondary protection:** ATO fuse holder (10 slots) for lines except ODrive.
- **Separate ODrive fuses:** 3 single holders with 80A fuses (one per ODrive3.6).
- **Voltages:** 25.9–29.4V (motors, directly), 19.5V (laptop), 5V (logic and display).

---

## Battery Pack Assembly

### Cells
- 7 Li‑NMC 3.7V 80.5Ah cells (SK) connected in series **7S1P**.
- Nominal voltage: **25.9V**, max fully charged: **29.4V**.
- Cell connections: aluminium/copper tabs are joined by **spot welding** (not soldering!). Cells are fixed in a rigid frame with compression (to prevent swelling).

### Inter‑block jumpers
- **Cable:** KGTP‑HL 1×10 mm² — for connecting separated groups.
- **Connectors:** XT90 pairs.

### Wiring from battery to BMS and breaker
- **Positive:** (+) → KGTP‑HL 1×10 → **DC breaker 200A** → distribution block 250A (+).
- **Negative:** (–) → KGTP‑HL 1×10 → BMS (–) → distribution block 250A (–).
- **Length:** 3 meters.

### Balance leads
- **Cable:** MGSHV 0.35 mm² — 20 m.
- **Terminals:** M6 ring terminals (8 pcs) — on each tab + common negative.
- Connect to BMS (configured for 7S).

### Fasteners and insulation
- Flanged nuts M6 with serrations — 16 pcs.
- Heat‑shrink tube 12mm (adhesive) — 1 m.

---

## Main Power Bus (25.9–29.4V)

### Primary distribution
After the 200A breaker, power goes to:
- **Positive block:** 250A, 12 terminals.
- **Negative block:** 250A, 12 terminals.

### ATO fuse holder (10 slots)
5 cables **KGTP‑HL 2×4 mm²** (12 m) connect the positive block to the fuse holder inputs:
- At distributor side: cores twisted together (≈8 mm²) → one NSHVI ferrule.
- At fuse holder side: cores separated → two 6.3 mm female terminals.
- 5 cables × 2 cores = 10 inputs.

### Load lines from ATO holder

| Line | Load | Fuse | Cable from holder to load |
| :--- | :--- | :---: | :--- |
| 1 | Buck 1500W → laptop (19.5V) | 25A | KGTP‑HL 2×1.5 |
| 2 | Buck 600W → LED display (5V) | 25A | KGTP‑HL 2×1.5 |
| 3 | Buck 300W → logic (5V) | 25A | KGTP‑HL 2×0.75 |
| 4 | Left arm — WAGO 5‑terminal | 40A | KGTP‑HL 2×4 |
| 5 | Right arm — WAGO 5‑terminal | 40A | KGTP‑HL 2×4 |
| 6 | Torso/abdomen — WAGO 3‑terminal | 40A | KGTP‑HL 2×4 |
| 7 | Head/neck — WAGO 3‑terminal | 10A | KGTP‑HL 2×1.5 |

**Important:** ODrive3.6 lines **do not go through the holder** – see separate section.

---

## Separate ODrive3.6 Protection (three units)

Each ODrive3.6 gets power through a dedicated holder with an 80A fuse.

- **Path:** Positive block 250A → KGTP‑HL 2×4 → **80A holder** → XT90 → **ODrive (Vin)**.
- **Negative:** ODrive (GND) → KGTP‑HL 2×4 → negative block 250A.
- **Cable length:** ~1.5–2 m.
- **Quantity:** 3 sets (left leg, right leg, waist).

---

## Secondary Wiring

- **KGTP‑HL 2×1.5 (10 m):** from WAGO to hoverboard boards, to bucks (input), from bucks to laptop, LED display, SimpleFOCMini.
- **KGTP‑HL 2×0.75 (5 m):** from 5V 300W buck to ESP32‑S3, GD32F303, BMI160, QMC5883L, other sensors.
- **MKEShng(A)‑LS 5×0.35 (15 m):** shielded signal (SPI, UART, CAN). Shield grounded at one point on negative block.

---

## Motor Phase Wiring

| Motor | Cable | Length |
| :--- | :--- | :---: |
| 6384 120KV (6 pcs) | KGTP‑HL 3×2.5 | 4 m |
| 5065 140KV (17 pcs) | KGTP‑HL 3×1.5 | 10 m |
| 3205 110KV (13 pcs) | KGTP‑HL 3×0.75 | 5 m |

---

## Capacitors and Filtering

- **Main bus buffer (torso):** 2× 50V 4700 µF between positive and negative blocks.
- **Buck output filters:** 3× 25V 1000 µF (on 19.5V, 5V 600W, 5V 300W).
- **Local driver protection (arms/neck):** 3× 50V 1000/4700 µF on WAGO.
- **HF decoupling:** 0.1 µF (104) on each SimpleFOCMini, MT6826S, BMI160.

---

## Connectors and Components

| Component | Qty | Purpose |
| :--- | :---: | :--- |
| Distribution block 250A (12‑terminal) | 2 | + and – bus bars |
| WAGO 221‑415 (5‑terminal) | 6 | Arms, neck/head |
| WAGO 221‑413 (3‑terminal) | 2 | Torso/abdomen |
| QS8P‑S (Anti‑Spark) | 1 pair | Between BMS and breaker |
| XT90 (pairs) | 6 pairs | ODrive and inter‑block connections |
| XT60/XT60h (pairs) | 12 pairs | Bucks, hoverboard boards |
| XT30 (pairs) | 5 pairs | SimpleFOCMini, neck drivers |
| GX12 (5‑pin, pairs) | 5 pairs | Signal (shielded) |
| JST‑XH 2.54 (set) | 1 | Sensors (BMI160, MT6826S) |

---

## Protection Summary

| Device | Qty | Location | Rating |
| :--- | :---: | :--- | :--- |
| DC breaker | 1 | After QS8P | 200A |
| ATO holder | 1 | After positive block | 10 slots |
| ATO 40A | 4 | Arms, torso (spare) | 40A |
| ATO 25A | 3 | Bucks (laptop, 5V 600W, 5V 300W) | 25A |
| ATO 10A | 1 | Head/neck | 10A |
| Single holder + 80A | 3 | Before each ODrive | 80A |

---

## Cable Summary

| Cable | Length |
| :--- | :---: |
| KGTP‑HL 1×10 | 3 m |
| KGTP‑HL 2×4 | 12 m |
| KGTP‑HL 2×1.5 | 10 m |
| KGTP‑HL 2×0.75 | 5 m |
| KGTP‑HL 3×2.5 | 4 m |
| KGTP‑HL 3×1.5 | 10 m |
| KGTP‑HL 3×0.75 | 5 m |
| MKEShng(A)‑LS 5×0.35 | 15 m |
| MKEShng(A)‑LS 2×0.35 | 5 m |
| MGSHV 0.35 | 20 m |

---

**Note:** Assembling a battery from pouch cells requires spot welding of tabs, a rigid compression frame, and a fireproof compartment.