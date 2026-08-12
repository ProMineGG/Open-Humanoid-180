# Power Distribution Schematics — Open-Humanoid-180

This document outlines the complete power distribution architecture for the robot — from the battery pack to every actuator, computing unit, and sensor.

---

## General Structure

- **Battery Pack:** 7S Li‑NMC (SK 3.7V 80.5Ah, pouch‑cells) — nominal 25.9V, max 29.4V (at 4.2V per cell).
- **BMS:** JK‑B2A8S20P (200A continuous, 7S support, one balance channel is left unused).
- **Main Protection:** 2-Pole (2P) DC automatic circuit breaker rated at 200A. Breaks both positive and negative rails simultaneously.
- **Distribution:** Two 250A power distribution blocks (12 terminals each) — positive and negative busbars.
- **Secondary Protection:** 10-slot ATO fuse hub for all load lines except ODrive controllers.
- **Dedicated ODrive Protection:** 3 single-slot fuse holders with 80A fuses (one for each ODrive3.6 board).
- **Voltages:** 25.9–29.4V (direct line to motors), 19.5V (laptop converter), 5V (logic units and LED screen).

---

## Battery Pack Assembly

### Cells
- 7 Li‑NMC 3.7V 80.5Ah pouch cells (SK) connected in series (**7S1P**).
- Nominal voltage: **25.9V**, maximum voltage at full charge: **29.4V**.
- Cell Interconnection: Cell power tabs must be carefully bent and overlapped using solid copper busbar links, secured tightly with M6 bolts and split lock washers (Grower washers) to prevent loosening from walking vibrations. The cells must be compressed inside a rigid structural frame to prevent swelling.

### Inter-Module Jumpers & Main Leads
- **Cable:** GOST-compliant **PuGV 1×25 mm²** flexible heavy-gauge wire — used for routing main high-current lines from cell tabs to the circuit breaker, BMS, and main distribution blocks.

### Battery-to-BMS and Breaker Wiring
- **Positive:** (+) → PuGV 1×25 mm² → **Input of the 1st pole of the 200A 2P Breaker** → Breaker Output → 250A Positive Distribution Block.
- **Negative:** (–) → PuGV 1×25 mm² → BMS (–) → BMS Output → **Input of the 2nd pole of the 200A 2P Breaker** → Breaker Output → 250A Negative Distribution Block.
- **Layout Note:** Routing the main 25 mm² PuGV bus through the 3 moving axes of the leg joints (in case of a potential battery relocation to the thighs) requires strict verification in CAD. Any potential layout modifications or swapping to high-flex silicone equivalents are frozen until the 3D-modeling phase.

### Balance Leads
- **Cable:** MGSHV 0.35 mm² wire — 20 m.
- **Terminals:** M6 ring crimp terminals (8 pcs) — mounted directly under the tab fastening bolts.
- Connected directly to the BMS JST connector (BMS configured to 7S operation).

### Fasteners & Insulation
- M6 flanged bolts and nuts with serration — 16 pcs.
- 12 mm dual-wall adhesive-lined heat shrink tubing — 1 m.
- Kapton / high-temperature insulation tape — 1 pc.

---

## Main Power Bus (25.9–29.4V)

### Primary Distribution
Past the 200A 2-pole circuit breaker, the main current splits into:
- **Positive Busbar:** 250A, 12-terminal block.
- **Negative Busbar:** 250A, 12-terminal block.

### ATO Fuse Hub (10 Slots)
5 dual-core **KGTP‑XL 2×4 mm²** cables (10 m total) link the positive busbar to the fuse hub inputs:
- On the busbar side, the two cores are twisted together (forming an 8 mm² equivalent) and crimped into a single pin cord-end terminal (NSHVI).
- On the fuse hub side, the cores separate into two 6.3 mm female spade quick-disconnect terminals.
- 5 cables × 2 cores = 10 individual fuse inputs.

### Load Lines Leaving the ATO Hub

| Line | Load / Sub-system | Fuse Rating | Cable Type (Hub to Load) |
| :--- | :--- | :---: | :--- |
| 1 | 1500W Step-Down Converter → Laptop (19.5V) | 25A | KGTP‑XL 2×1.5 |
| 2 | 600W Step-Down Converter → LED Screen (5V) | 25A | KGTP‑XL 2×1.5 |
| 3 | 300W Step-Down Converter → Central Logic Power Hub (5V) | 25A | KGTP‑XL 2×1.5 |
| 4 | Left Arm — 5-pin WAGO terminal (SimpleFOC supply) | 40A | KGTP‑XL 2×4 |
| 5 | Right Arm — 5-pin WAGO terminal (SimpleFOC supply) | 40A | KGTP‑XL 2×4 |
| 6 | Torso/Abdomen — 3-pin WAGO terminal | 40A | KGTP‑XL 2×4 |
| 7 | Head/Neck — 3-pin WAGO terminal | 10A | KGTP‑XL 2×1.5 |

**Important Notice:** All lines powering the ODrive3.6 controllers **bypass the main ATO fuse hub completely** — see the dedicated section below.

---

## Dedicated ODrive3.6 Protection (3 Units)

Each ODrive3.6 controller is powered via an independent inline fuse holder populated with an 80A fuse.

- **Circuit:** Positive Busbar (250A) → KGTP‑XL 2×4 → **80A Fuse Holder** → XT90 Connector → **ODrive (Vin)**.
- **Negative:** ODrive (GND) → KGTP‑XL 2×4 → Negative Busbar (250A).
- **Cable Length:** ~1.5–2 m per run.
- **Quantity:** 3 complete matching wiring runs (Left Leg, Right Leg, Lower Back/Waist).

---

## Secondary & Logic Wiring

- **KGTP‑XL 2×1.5 (10 m):** Stationary internal housing wiring. Runs from WAGO terminal blocks to hoverboard driver boards, to buck converter inputs, and from converters to the laptop, LED screen, and SimpleFOCMini boards.
- **MGSHV 0.35 mm² (20 m):** Local point-to-point interconnect wiring, prototyping jumpers, and low-current power routing inside enclosed hub boxes and control boards.
- **MKESHng(A)‑LS 7×0.35 (20 m):** Shielded multi-core trunk line for SPI sensor buses. Used to route signals from the 11 IMU modules (BMI160 + localized slave QMC5883L via local I2C), MT6826S magnetic joint encoders, and outputs from the CD74HC4067 analog multiplexers hidden inside the hands. 2 internal wires are dedicated to a localized +5V and GND logic power transit.
- **MKESHng(А)‑LS 5×0.35 (15 m):** High-speed transit for inter-board communication (CAN-bus linking AT32 hubs to the central ESP32-S3 / UART lines). Also handles the digital output data coming from the HX711 ADC boards installed inside the feet (digitizing the dual 100 kg load cells). 2 internal wires are dedicated to a localized +5V and GND logic power transit.
- **MKESHng(А)‑LS 2×0.35 (5 m):** Simplified connections for isolated limit switches, foot contact bumpers, and the physical Emergency Stop (E-Stop) master button.
- **Shield Grounding:** The braided copper shielding of all MKESH cables must be tied to a single, common ground point on the main negative distribution block. This prevents high-frequency PWM switching noise generated by the FOC motor drivers from introducing corruption into the logic sensor buses.

---

## Actuator Phase Wiring (Super-Flexible Silicone AWG)

All motor phase wiring running through moving joint pivots utilizes high-strand silicone insulation to eliminate mechanical spring-back forces against the PTK wave reducers and safeguard the copper lines against fatigue snapping.

| Actuator Motor | Cable Type | Total Strand Metrage | Installation & Routing Notes |
| :--- | :--- | :---: | :--- |
| **6384 120KV (6 pcs)** <br>Heavy-duty leg joints | Silicone **14 AWG** (2.08 mm²) | ~25 m | Twisted into 3-phase tight braids; routed via a loose U-shaped loop along the exterior curve of the hinge joints. |
| **5065 140KV (7 pcs)** <br>Pelvis & hip actuators | Silicone **14 AWG** (2.08 mm²) | ~25 m | Harmonized with 6384 gauge. Guarantees ampacity margin under continuous FOC hold loads supporting the upper body. |
| **5010 330KV (10 pcs)** <br>Mid-tier arm actuators | Silicone **20 AWG** (0.52 mm²) | 50 m (Box) | Phases assembled into 3-color matching braids using the sorted storage box. Rated up to 11A continuous. |
| **2805 110KV (13 pcs)** <br>Finger servos & neck | Silicone **26 AWG** (0.13 mm²) | 50 m (Box) | Ultra-thin phase strands. Minimizes wire cluster bulk inside the palms to feed 5 active fingers cleanly. |

---

## Capacitors and Filtering

- **Main Bus Buffer (Torso):** 2× 50V 4700 μF low-ESR capacitors mounted directly across the positive and negative distribution blocks.
- **Buck Converter Output Filters:** 3× 25V 1000 μF capacitors (on the 19.5V run, 5V 600W run, and 5V 300W run).
- **Localized Driver Protection (Arms/Neck):** 3× 50V 1000/4700 μF capacitors installed at the local WAGO distribution nodes.
- **HF Decoupling:** 0.1 μF (104 ceramic) bypass capacitors placed immediately at the power pins of each SimpleFOCMini, MT6826S, and BMI160 chip.

---

## Connectors and Hard Components

| Component                        |   Qty    | Intended Application / Connection Node                                               |     |
| :------------------------------- | :------: | :----------------------------------------------------------------------------------- | --- |
| 250A Distro Block (12 terminals) |    2     | Primary + and – power distribution busbars in the torso                              |     |
| CD74HC4067 Multiplexer Board     |    2     | Localized multiplexed sampling of FSR402 pressure pads inside the hands (1 per hand) |     |
| HX711 ADC Breakout Board         |    2     | Localized digitizing of analog load cell signals inside the feet (1 per foot)        |     |
| WAGO 221‑415 (5-wire lever)      |    6     | Secondary power distribution splits inside the arms and neck                         |     |
| WAGO 221‑413 (3-wire lever)      |    2     | Secondary power distribution splits inside the torso cavity                          |     |
| QS8P‑S (Anti‑Spark)              |  1 pair  | Master manual battery disconnect plug situated upstream of the main breaker          |     |
| XT90-S (Anti-Spark)              | 4 pairs  | Quick-disconnect points for transit power lines traveling from thighs to torso       |     |
| XT90 (Standard pairs)            | 6 pairs  | Main inputs for ODrive controllers and primary sub-assembly interfaces               |     |
| XT60/XT60h (Standard pairs)      | 12 pairs | Input/output hooks for buck converters and hoverboard driver boards                  |     |
| XT30 (Standard pairs)            | 5 pairs  | Power feeds to SimpleFOCMini modules and neck actuators                              |     |
| GX12 (5-pin, panel-mount pairs)  | 5 pairs  | Shielded low-frequency signal interconnects between structural chassis blocks        |     |
| JST‑XH 2.54 (Assorted Kit)       |    1     | Micro-crimping connectors for encoder and logic breakout lines (BMI160, MT6826S)     |     |

---

## Protection Fuse Matrix Summary

|Protection Device|Qty|Physical Mounting Location|Rated Trip Current|
|---|---|---|---|
|DC 2-Pole Circuit Breaker|1|Inline past the master QS8P plug; cuts (+) and (–) simultaneously|200A|
|ATO Blade Fuse Hub|1|Positioned immediately downstream of the positive 250A block|10 Slots Available|
|ATO Blade Fuse 40A|4|Protecting the Arm WAGO nodes and main Torso lines|40A|
|ATO Blade Fuse 25A|3|Protecting Buck Converters (Laptop, 5V 600W, 5V 300W)|25A|
|ATO Blade Fuse 10A|1|Protecting Head, Neck, and localized logic nodes|10A|
|Inline Holder + ANL/MIDI 80A|3|Dedicated protection module placed immediately before each ODrive3.6 input|80A|

---

## Cable Ledger Summary

|Cable Ledger Designation|Required Length|Supplier Target|Intended Routing Target|
|---|---|---|---|
|PuGVng-LS 1×25 mm²|3 m|Cable-ES|Primary heavy-current links from cells to BMS, 2P breaker, and main busbars|
|KGTP‑XL 2×4|10 m|Cable-ES|Stationary high-current runs feeding the ATO fuse block and local ODrive inputs|
|KGTP‑XL 2×1.5|10 m|Cable-ES|Stationary runs feeding hoverboard inputs and buck converter lines|
|MKESHng(А)‑LS 7×0.35|20 m|Cable-ES|Shielded SPI data runs (IMU modules, encoders, multiplexers) + embedded 5V logic|
|MKESHng(А)‑LS 5×0.35|15 m|Cable-ES|Shielded CAN-bus lines between hubs, UART lines, and digitized foot cell inputs|
|MKESHng(А)‑LS 2×0.35|5 m|Cable-ES|Shielded isolated lines for hard limit switches, bumpers, and the E-Stop loop|
|MGSHV 0.35|20 m|Cable-ES|BMS cell balancing leads and tight point-to-point electronic enclosure wiring|
|Silicone 14 AWG (2.08 mm²)|50 m|Ozon (Kit)|High-flex phase wires for high-torque leg/pelvis BLDC motors (6384 and 5065)|
|Silicone 20 AWG (0.52 mm²)|50 m|Ozon (Kit)|High-flex phase wires for arm BLDC actuators (10 units of 5010 330KV)|
|Silicone 26 AWG (0.13 mm²)|50 m|Ozon (Kit)|Ultra-flex phase wires for micro finger BLDC actuators and neck servos (13 units of 2805)|

---

**Engineering Notice**: Designing and assembling a custom battery pack from pouch-style cells requires a robust structural enclosure capable of maintaining exact mechanical compression on the cell faces, combined with an isolated, flame-retardant bay. Cell tabs must be bolted using copper links and lock washers. If the pack is split or moved into the thigh regions during CAD, 3D cable spine simulations are mandatory to verify that the massive 25 mm² PuGV conductors can clear the internal bend radius thresholds of the hip joints without locking up the degrees of freedom.