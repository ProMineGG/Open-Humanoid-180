# Power Distribution Schematics — Open-Humanoid-180

This document outlines the complete power distribution architecture for the robot — from the battery pack to every actuator, computing unit, and sensor.

---

## General Structure

- **Battery Pack:** 10S Li‑NMC (SK 3.7V 80.5Ah, pouch‑cells) — nominal 37V, max 42V (cell voltage limited to 3.3–4.1V via BMS for longevity).
- **BMS:** JK‑B2A24S20P (200A continuous, 8‑24S support) with Bluetooth monitoring.
- **Main Protection:** 2‑Pole (2P) DC automatic circuit breaker rated at 200A. Breaks both positive and negative rails simultaneously.
- **Distribution:** Two 250A power distribution blocks (11 terminals each) — positive and negative busbars.
- **Secondary Protection:** 10‑slot ATO fuse hub for all load lines except ODrive controllers.
- **Dedicated ODrive Protection:** 3 single‑slot fuse holders with 80A fuses (one for each ODrive3.6 board).
- **Voltages:** 33–41V (motors 6384, 5065, 5010), 24V (SimpleFOCmini), 20V (laptop), 5V (logic and display).

---

## Battery Pack Assembly

### Cells
- 10 Li‑NMC 3.7V 80.5Ah pouch cells (SK) connected in series (**10S1P**).
- Nominal voltage: **37V**, maximum voltage at full charge: **42V**.
- Cell Interconnection: Cell power tabs must be carefully bent and overlapped using solid copper busbar links, secured tightly with M6 bolts and split lock washers (Grower washers) to prevent loosening from walking vibrations. The cells must be compressed inside a rigid structural frame to prevent swelling.

### Inter‑Module Jumpers & Main Leads
- **Cable:** Flexible heavy‑gauge wire **KOG1‑T 1×25 mm²** — used for routing main high‑current lines from cell tabs to the circuit breaker, BMS, and main distribution blocks.

### Battery‑to‑BMS and Breaker Wiring
- **Positive:** (+) → KOG1‑T 1×25 mm² → **Input of the 1st pole of the 200A 2P Breaker** → Breaker Output → 250A Positive Distribution Block.
- **Negative:** (–) → KOG1‑T 1×25 mm² → BMS (–) → BMS Output → **Input of the 2nd pole of the 200A 2P Breaker** → Breaker Output → 250A Negative Distribution Block.
- **Layout Note:** Routing the main 25 mm² KOG1‑T bus through the moving axes of the leg joints requires strict verification in CAD. Any potential layout modifications or swapping to high‑flex silicone equivalents are frozen until the 3D‑modeling phase.

### Balance Leads
- **Cable:** 30 AWG silicone wire — 10 m.
- **Terminals:** M6 ring terminals (8 pcs) — mounted directly under the tab fastening bolts.
- Connected directly to the BMS (configured to 10S operation).

### Fasteners & Insulation
- M6 flanged bolts and nuts with serration — 16 pcs.
- M6 Grower washers — 16 pcs.
- 12 mm dual‑wall adhesive‑lined heat shrink tubing — 1 m.
- Kapton / high‑temperature insulation tape — 1 pc.

---

## Main Power Bus (33–41V)

### Primary Distribution
Past the 200A 2‑pole circuit breaker, the main current splits into:
- **Positive Busbar:** 250A, 11‑terminal block.
- **Negative Busbar:** 250A, 11‑terminal block.

### ATO Fuse Hub (10 Slots)
5 dual‑core **KGTP‑HL 2×4 mm²** cables (10 m total) link the positive busbar to the fuse hub inputs:
- On the busbar side, the two cores are twisted together (forming an 8 mm² equivalent) and crimped into a single pin cord‑end terminal (NSHVI).
- On the fuse hub side, the cores separate into two 6.3 mm female spade quick‑disconnect terminals.
- 5 cables × 2 cores = 10 individual fuse inputs.

### Load Lines Leaving the ATO Hub

| Line | Load / Sub‑system | Fuse Rating | Cable Type (Hub to Load) |
| :--- | :--- | :---: | :--- |
| 1 | 1500W Step‑Down Converter → Laptop (20V) | 25A | KGTP‑HL 2×1.5 |
| 2 | 600W Step‑Down Converter → LED Screen (5V) | 25A | KGTP‑HL 2×1.5 |
| 3 | 300W Step‑Down Converter → Central Logic Power Hub (5V) | 25A | KGTP‑HL 2×1.5 |
| 4 | Left Arm — 5‑pin WAGO terminal (SimpleFOC supply) | 40A | KGTP‑HL 2×4 |
| 5 | Right Arm — 5‑pin WAGO terminal (SimpleFOC supply) | 40A | KGTP‑HL 2×4 |
| 6 | Torso/Abdomen — 3‑pin WAGO terminal | 40A | KGTP‑HL 2×4 |
| 7 | Head/Neck — 3‑pin WAGO terminal | 10A | KGTP‑HL 2×1.5 |

**Important Notice:** All lines powering the ODrive3.6 controllers **bypass the main ATO fuse hub completely** — see the dedicated section below.

---

## Dedicated ODrive3.6 Protection (3 Units)

Each ODrive3.6 controller is powered via an independent inline fuse holder populated with an 80A fuse.

- **Circuit:** Positive Busbar (250A) → KGTP‑HL 2×4 → **80A Fuse Holder** → XT90 Connector → **ODrive (Vin)**.
- **Negative:** ODrive (GND) → KGTP‑HL 2×4 → Negative Busbar (250A).
- **Cable Length:** ~1.5–2 m per run.
- **Quantity:** 3 complete matching wiring runs (Left Leg, Right Leg, Lower Back/Waist).

---

## Secondary & Logic Wiring

- **KGTP‑HL 2×1.5 (10 m):** Stationary internal housing wiring. Runs from WAGO terminal blocks to hoverboard driver boards, to buck converter inputs, and from converters to the laptop, LED screen, and SimpleFOCMini boards.
- **MGSHV 0.35 mm² (20 m):** Local point‑to‑point interconnect wiring, prototyping jumpers, and low‑current power routing inside enclosed hub boxes and control boards.
- **MKEShng(A)‑LS 7×0.35 (20 m):** Shielded multi‑core trunk line for SPI sensor buses. Used to route signals from the 13 BMI160 IMU modules, MT6826S magnetic joint encoders, and outputs from the CD74HC4067 analog multiplexers hidden inside the hands. 2 internal wires are dedicated to a localized +5V and GND logic power transit.
- **MKEShng(А)‑LS 5×0.35 (15 m):** High‑speed transit for inter‑board communication (CAN‑bus linking AT32/STM32 hubs to the central ESP32‑S3 / UART lines). Also handles the digital output data coming from the HX711 ADC boards installed inside the feet (digitizing the dual 100 kg load cells). 2 internal wires are dedicated to a localized +5V and GND logic power transit.
- **MKEShng(А)‑LS 2×0.35 (5 m):** Simplified connections for isolated limit switches, foot contact bumpers, and the physical Emergency Stop (E‑Stop) master button.
- **Shield Grounding:** The braided copper shielding of all MKESh cables must be tied to a single, common ground point on the main negative distribution block. This prevents high‑frequency PWM switching noise generated by the FOC motor drivers from introducing corruption into the logic sensor buses.

---

## Actuator Phase Wiring (Super‑Flexible Silicone AWG)

All motor phase wiring running through moving joint pivots utilizes high‑strand silicone insulation to eliminate mechanical spring‑back forces against the PTK wave reducers and safeguard the copper lines against fatigue snapping.

| Actuator Motor | Cable Type | Total Strand Metrage | Installation & Routing Notes |
| :--- | :--- | :---: | :--- |
| **6384 120KV (6 pcs)** <br>Heavy‑duty leg joints | Silicone **14 AWG** (2.08 mm²) | ~25 m | Twisted into 3‑phase tight braids; routed via a loose U‑shaped loop along the exterior curve of the hinge joints. |
| **5065 140KV (7 pcs)** <br>Pelvis & hip actuators | Silicone **14 AWG** (2.08 mm²) | ~25 m | Harmonized with 6384 gauge. Guarantees ampacity margin under continuous FOC hold loads supporting the upper body. |
| **5010 330KV (10 pcs)** <br>Mid‑tier arm actuators | Silicone **20 AWG** (0.52 mm²) | 50 m | Phases assembled into 3‑color matching braids. Rated up to 11A continuous. |
| **3205 110KV (13 pcs)** <br>Finger servos & neck | Silicone **26 AWG** (0.13 mm²) | 50 m | Ultra‑thin phase strands. Minimizes wire cluster bulk inside the palms to feed 5 active fingers cleanly. |

---

## Capacitors and Filtering

- **Local Driver Protection:** 10× 4700 µF / 63V capacitors placed near ODrive 3.6 and hoverboard driver boards; 13× 4700 µF / 35V capacitors near SimpleFOCMini boards.
- **Buck Output Filters:** LC filters on the 5V logic rail (4A) and the 24V SimpleFOCmini rail (20A).
- **HF Decoupling:** 0.1 µF (104 ceramic) bypass capacitors placed immediately at the power pins of each SimpleFOCMini, MT6826S, and BMI160 chip.

---

## Connectors and Hard Components

| Component                        |   Qty    | Intended Application / Connection Node                                               |
| :------------------------------- | :------: | :----------------------------------------------------------------------------------- |
| 250A Distro Block (11 terminals) |    2     | Primary + and – power distribution busbars in the torso                              |
| CD74HC4067 Multiplexer Board     |    2     | Localized multiplexed sampling of FSR402 pressure pads inside the hands (1 per hand) |
| HX711 ADC Breakout Board         |    2     | Localized digitizing of analog load cell signals inside the feet (1 per foot)        |
| WAGO 221‑415 (5‑wire lever)      |    6     | Secondary power distribution splits inside the arms and neck                         |
| WAGO 221‑413 (3‑wire lever)      |    2     | Secondary power distribution splits inside the torso cavity                          |
| QS8P‑S (Anti‑Spark)              |  1 pair  | Master manual battery disconnect plug situated upstream of the main breaker          |
| XT90-S (Anti-Spark)              | 4 pairs  | Quick‑disconnect points for transit power lines traveling from thighs to torso       |
| XT90 (Standard pairs)            | 6 pairs  | Main inputs for ODrive controllers and primary sub‑assembly interfaces               |
| XT60/XT60h (Standard pairs)      | 12 pairs | Input/output hooks for buck converters and hoverboard driver boards                  |
| XT30 (Standard pairs)            | 5 pairs  | Power feeds to SimpleFOCMini modules and neck actuators                              |
| GX12 (5‑pin, panel‑mount pairs)  | 5 pairs  | Shielded low‑frequency signal interconnects between structural chassis blocks        |
| JST‑XH 2.54 (Assorted Kit)       |    1     | Micro‑crimping connectors for encoder and logic breakout lines (BMI160, MT6826S)     |

---

## Protection Fuse Matrix Summary

| Protection Device                 | Qty | Physical Mounting Location                                | Rated Trip Current |
| :-------------------------------- | :-: | :-------------------------------------------------------- | :----------------: |
| DC 2‑Pole Circuit Breaker         |  1  | Inline past the master QS8P plug; cuts (+) and (–) simultaneously | 200A              |
| ATO Blade Fuse Hub                |  1  | Positioned immediately downstream of the positive 250A block      | 10 Slots Available |
| ATO Blade Fuse 40A                |  4  | Protecting the Arm WAGO nodes and main Torso lines          | 40A               |
| ATO Blade Fuse 25A                |  3  | Protecting Buck Converters (Laptop, 5V 600W, 5V 300W)       | 25A               |
| ATO Blade Fuse 10A                |  1  | Protecting Head, Neck, and localized logic nodes            | 10A               |
| Inline Holder + ANL/MIDI 80A      |  3  | Dedicated protection module placed immediately before each ODrive3.6 input | 80A |

---

## Cable Ledger Summary

| Cable Designation                  | Required Length | Supplier Target | Intended Routing Target                                                                 |
| :--------------------------------- | :-------------: | :-------------: | :-------------------------------------------------------------------------------------- |
| KOG1‑T 1×25 mm²                    |      3 m        |    Cable‑ES     | Primary heavy‑current links from cells to BMS, 2P breaker, and main busbars              |
| KGTP‑HL 2×4                        |      10 m       |    Cable‑ES     | Stationary high‑current runs feeding the ATO fuse block and local ODrive inputs          |
| KGTP‑HL 2×1.5                      |      10 m       |    Cable‑ES     | Stationary runs feeding hoverboard inputs and buck converter lines                       |
| MKEShng(A)‑LS 7×0.35               |      20 m       |    Cable‑ES     | Shielded SPI data runs (IMU modules, encoders, multiplexers) + embedded 5V logic         |
| MKEShng(A)‑LS 5×0.35               |      15 m       |    Cable‑ES     | Shielded CAN‑bus lines between hubs, UART lines, and digitized foot cell inputs          |
| MKEShng(A)‑LS 2×0.35               |       5 m       |    Cable‑ES     | Shielded isolated lines for hard limit switches, bumpers, and the E‑Stop loop            |
| MGSHV 0.35                         |      20 m       |    Cable‑ES     | BMS cell balancing leads and tight point‑to‑point electronic enclosure wiring            |
| Silicone 14 AWG (2.08 mm²)         |      50 m       |  Ozon (Kit)     | High‑flex phase wires for high‑torque leg/pelvis BLDC motors (6384 and 5065)             |
| Silicone 20 AWG (0.52 mm²)         |      50 m       |  Ozon (Kit)     | High‑flex phase wires for arm BLDC actuators (10 units of 5010)                          |
| Silicone 26 AWG (0.13 mm²)         |      50 m       |  Ozon (Kit)     | Ultra‑flex phase wires for micro finger BLDC actuators and neck servos (13 units of 3205) |
| Silicone 30 AWG (0.05 mm²)         |      50 m       |  Ozon (Kit)     | CAN, balance leads, logic                                                               |

---

**Engineering Notice:** Designing and assembling a custom battery pack from pouch‑style cells requires a robust structural enclosure capable of maintaining exact mechanical compression on the cell faces, combined with an isolated, flame‑retardant bay. Cell tabs must be bolted using copper links and lock washers. If the pack is split or moved into the thigh regions during CAD, 3D cable spine simulations are mandatory to verify that the massive 25 mm² KOG1‑T conductors can clear the internal bend radius thresholds of the hip joints without locking up the degrees of freedom.