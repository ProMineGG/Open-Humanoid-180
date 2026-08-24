# Component Weight Budget — Open-Humanoid-180

This document contains the up-to-date weight breakdown calculation for the robot by component category, reflecting the active power layout and the new actuator configuration (36 degrees of freedom).  
All weights are based on manufacturer data sheets, actual component measurements, or justified engineering estimates.

**Target Weight:** ~45–50 kg.  
**Calculated Weight:** ~51–52 kg (successfully minimized by switching to lightweight motors and compact silicone wiring).

---

## Motors

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| BLDC 6384 120KV (Heavy-duty, legs) | 6 | 0.650 | 3.90 | High-power belt/girdle zone (knees/thighs) |
| BLDC 5065 140KV (Medium-heavy, pelvis/torso) | 7 | 0.350 | 2.45 | High-torque actuators for large articulation joints |
| BLDC 5010 330KV (Base, arms/elbows) | 10 | 0.080 | 0.80 | Lightweight "pancake" form-factor with good torque density |
| BLDC 3205 110KV (Low-power, fingers/neck) | 13 | 0.035 | 0.455 | Miniature actuators for fine mechanics and joints |
| **Motors Total** | | | **7.605** |  |

---

## Motor Drivers

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| ODrive3.6 (Clone, legs) | 3 | 0.060 | 0.18 | Drives the 6384 motors (2 channels per board) |
| Hoverboard Driver Board (2 channels) | 9 | 0.100 | 0.90 | Drives the 5065 and 5010 motor groups |
| SimpleFOCMini (MS8313) | 13 | 0.010 | 0.13 | Tiny driver boards for the fingers and neck (3205) |
| **Drivers Total** | | | **1.21** |  |

---

## Sensors

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| MT6826S Magnetic Encoder | 36 | 0.002 | 0.072 | FOC feedback tracking modules for each motor |
| 9-Axis IMU BMI160 (+ QMC5883L) | 11 | 0.002 | 0.022 | Distributed localized telemetry modules |
| FSR402 Pressure Sensor (Fingers) | 10 | 0.001 | 0.010 | Thin-film resistors built into the hands |
| Foot Load Cell 100 kg | 4 | 0.010 | 0.040 | 2 individual weight load cells per foot |
| HX711 ADC Breakout Board | 2 | 0.002 | 0.004 | Localized digital conversion boards inside the feet |
| Dual HD USB Camera (OV4689) | 1 | 0.030 | 0.030 | AI vision system (paired with 3mm zero lenses) |
| **Sensors Total** | | | **0.178** |  |

---

## Computing & Logic Hubs

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Laptop Motherboard (RTX 3080 / 32GB / 1TB) | 1 | 0.850 | 0.850 | Stripped down motherboard without chassis or display (VLM/YOLO/ROS2) |
| ESP32‑S3 N16R8 | 1 | 0.010 | 0.010 | Main low-level master controller |
| AT32F403A Bridge-MCU Board | 7 | 0.005 | 0.035 | Distributed localized CAN-bus hubs |
| CD74HC4067 Analog Multiplexer | 2 | 0.002 | 0.004 | Localized sensor data routing inside the hands |
| **Logic Total** | | | **0.899** |  |

---

## Battery & Power Routing Modules

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Li‑NMC 3.7V 80.5Ah (SK Pouch Cell) | 7 | 0.900 | 6.300 | Primary 7S1P high-capacity power pack |
| JK‑B2A8S20P BMS (8S, 200A) | 1 | 0.200 | 0.200 | Battery block configuration management system |
| 1500W Step-Down DC-DC (28.8→19.5V) | 1 | 0.300 | 0.300 | Heavy duty converter feeding the RTX 3080 |
| 600W Step-Down DC-DC (28.8→5V) | 1 | 0.150 | 0.150 | Feeds the active LED matrix screen |
| 300W Step-Down DC-DC (28.8→5V) | 1 | 0.100 | 0.100 | Clean power line feeding logic buses & sensors |
| **Battery & Power Total** | | | **7.05** |  |

---

## Cables (Silicone + Industrial GOST)

*Weight is calculated based on the actual linear mass densities of multi-strand copper conductors and insulation layers.*

| Cable Specification / Gauge | Length | Weight per Meter (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| PuGVng-LS 1×25 mm² Heavy-Gauge | 3 m | 0.290 | 0.870 | Primary high-current rail (Battery -> BMS -> Breaker -> Distro) |
| KGTP-XL 2×4 mm² Dual-Core | 10 m | 0.150 | 1.500 | Stationary high-amperage lines to ATO hub and ODrives |
| KGTP-XL 2×1.5 mm² Dual-Core | 10 m | 0.080 | 0.800 | Stationary lines feeding hoverboard drivers and DC-DC blocks |
| MKESHng(A)-LS 7×0.35 mm² Shielded | 20 m | 0.065 | 1.300 | Braided copper SPI buses (IMUs, encoders) + logic 5V power |
| MKESHng(A)-LS 5×0.35 mm² Shielded | 15 m | 0.050 | 0.750 | Braided copper CAN-bus hubs and HX711 foot data feeds |
| MKESHng(A)-LS 2×0.35 mm² Shielded | 5 m | 0.030 | 0.150 | Isolated limit switch lines, bumpers, and E-Stop loops |
| MGSHV 0.35 mm² Wire | 20 m | 0.006 | 0.120 | BMS cell balancing cables + localized tight enclosure wiring |
| Silicone 14 AWG (2.08 mm²) High-Flex | 50 m | 0.032 | 1.600 | Phase wiring for high-torque leg/hip BLDC motors (6384 & 5065) |
| Silicone 20 AWG (0.52 mm²) High-Flex | 50 m | 0.011 | 0.550 | Phase wiring for mid-tier arm BLDC actuators (10× 5010) |
| Silicone 26 AWG (0.13 mm²) High-Flex | 50 m | 0.004 | 0.200 | Ultra-fine phase wiring for finger BLDC servos and neck (13× 3205) |
| **Cables Total** | | | **7.84** |  |

---

## Connectors & Interconnect Terminals

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| 250A Power Distribution Block (12-term) | 2 | 0.150 | 0.300 | Solid brass-steel power busbars inside the torso |
| WAGO 221‑415 (5-wire lever) | 6 | 0.015 | 0.090 | Power distribution splits inside the arms and neck |
| WAGO 221‑413 (3-wire lever) | 2 | 0.010 | 0.020 | Power distribution splits inside the central torso cavity |
| QS8P‑S (Anti‑Spark Module) | 1 pair | 0.050 | 0.050 | Master battery manual disconnect coupling |
| XT90-S / XT90 Connector Pairs | 10 | 0.020 | 0.200 | Inter-chassis leg transit lines and ODrive links |
| XT60 Connector Pairs | 12 | 0.010 | 0.120 | Buck converter and hoverboard driver interface points |
| XT30 Connector Pairs | 5 | 0.005 | 0.025 | Interconnects feeding SimpleFOCMini modules |
| GX12 Panel Connectors (5-pin pairs) | 5 | 0.015 | 0.075 | Robust structural logic chassis disconnect nodes |
| JST‑XH 2.54 mm Interface Kit | 1 | 0.020 | 0.020 | Low-power sensor PCB connection array |
| **Connectors Total** | | | **0.90** |  |

---

## Fuse Hardware & System Protection

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| DC 2P Circuit Breaker 200A | 1 | 0.350 | 0.350 | Master heavy-duty dual-pole automatic breaker module |
| ATO Blade Fuse Block (10 Slots) | 1 | 0.050 | 0.050 | Secondary current management hub |
| ATO Blade Fuses (40A, 25A, 10A arrays) | 10 | 0.002 | 0.020 | Sacrificial current overcurrent fuse links |
| Inline Single Fuse Holders (w/ 80A Fuses) | 3 | 0.020 | 0.060 | Isolated protection runs dedicated to individual ODrives |
| **Protection Total** | | | **0.48** |  |

---

## Power Filters & Capacitors

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Aluminum Electrolytic 50V 4700 μF | 6 | 0.015 | 0.090 | Bulk storage filter banks for the main high-power bus |
| Aluminum Electrolytic 25V 1000 μF | 10 | 0.005 | 0.050 | Smoothing output filters down the DC-DC converter lines |
| Ceramic Capacitors 50V 0.1 μF | 100 | 0.0005 | 0.050 | SMD bypass decoupling to counter HF driver noise |
| Hardware Resistors Array | 1 kit | 0.020 | 0.020 | General bleeding/pull-down array |
| **Filtering Total** | | | **0.21** |  |

---

## Display Matrix

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| P1.53 Flexible LED Panel (320×160 mm) | 1 | 0.200 | 0.200 | Dynamic expression matrix face panel |
| **Display Total** | | | **0.20** |  |

---

## Chassis Structure & Printing Materials

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| PETG Filament (Net Printed Part Weight) | — | — | 6.000 | External paneling, protection fairings, shroud layers |
| TPU A95 Flex-Filament (Net Printed Weight) | — | — | 1.000 | Vibration dampening gaskets, soft isolators, foot outsoles |
| PA12‑CF Carbon-Filled Nylon | — | — | 1.200 | Structural bearing seats, high-load arm shell matrices |
| Dual-Component Polyurethane/Silicone | — | — | 0.500 | Cast dampening areas and soft interface linings |
| Cast Aluminum (Skeleton Brackets / Mounts) | — | — | 3.500 | Core weight-bearing framework of hips, pelvis, and torso |
| Aluminum Tubing (Primary Chassis Spine) | — | — | 3.000 | Rigid extrusion long-runs feeding legs and spine lines |
| **Structure Total** | | | **15.20** |  |

---

## Hardware Fasteners & Spacers

| Component | Qty | Unit Weight (kg) | Total (kg) | Notes |
| :--- | :---: | :---: | :---: | :--- |
| Fasteners Matrix Set (M3, M4, M5, M6 arrays) | 1 kit | 0.500 | 0.500 | Total mass of high-tensile metal assembly screws |
| Solid Copper Connecting Links (Battery E805) | 8 | 0.015 | 0.120 | Custom custom cut bars out of electrical grade sheeting |
| M6 Flanged Tab Bolts and Matching Nuts | 16 | 0.005 | 0.080 | Secure compression fasteners linking cell tabs together |
| Heavy-Duty Ties, Shrink, and Electrical Wrap | 1 kit | 0.200 | 0.200 | General loom grouping and terminal isolation wraps |
| **Fasteners Total** | | | **0.90** |  |

---

## Strain Wave Reducers with PTK (36 Units)

_Mass calculation of joints incorporating steel intermediate rolling elements (rollers) and cast aluminum separator housings._

|Joint Application Node|Qty|Reduction Ratio|Unit Weight (kg)|Total (kg)|Notes|
|---|---|---|---|---|---|
|High-Torque Pivot (Legs/Knees) for 6384|6|1:100|0.500|3.00|Massive load rollers, maximized shell thickness|
|Mid-Torque Pivot (Pelvis/Shoulders) for 5065|7|1:65|0.300|2.10|Moderate shell profile, compact tracker|
|Standard Pivot (Elbows/Arms) for 5010|10|1:65 / 1:40|0.200|2.00|Specialized compact and slim profile housing lines|
|Miniature Pivot (Fingers/Neck) for 3205|13|1:40|0.080|1.04|Ultra-miniature custom wave-gear rolling sets|
|Reducers Total||||8.14||

---

## Consolidated Weight Summary Matrix

|Category Hub|Net Mass (kg)|Total Allocation %|
|---|---|---|
|Motors|7.605|14.8%|
|Drivers|1.210|2.4%|
|Sensors|0.178|0.3%|
|Logic Array|0.899|1.7%|
|Battery & Power Units|7.050|13.7%|
|Cable Runs Matrix|7.840|15.2%|
|Connectors|0.900|1.7%|
|Protection Devices|0.480|0.9%|
|Filtering Modules|0.210|0.4%|
|Expressions Screen|0.200|0.4%|
|Structural Material|15.200|29.5%|
|Fasteners Set|0.900|1.7%|
|Strain Wave Reducers (36 Units)|8.140|15.8%|
|TOTAL ASSEMBLY MASS|~50.81 kg|100%|

---

## Engineering Considerations for CAD Modeling Trace

- The Cable Mass Trap: Keep in mind that the cumulative weight of the cable tracks (7.84 kg) has officially surpassed the combined net weight of all 36 electric motors on the robot (7.605 kg). This is the unforgiving reality of scaling 1:1 humanoid electronics. Large silicone jackets and braided copper shielding inside the MKESH runs pack massive weight densities; slice away every redundant centimeter during CAD wire routing.
- Pelvic Center of Mass Offset: Given that the upper cavity is heavily saturated with the naked RTX 3080 board, the hefty 2P circuit breaker, distribution bars, and massive core torso gears, the true center of mass is heavily biased upward. The 6.3 kg pouch battery assembly must be mathematically mapped and locked inside a rigid, symmetrical matrix down the thigh structures to act as a counterweight if torso space proves entirely inadequate.
- Structural Mass Trimming Optimization: If the physical top-level assembly calculation breaks beyond the 52 kg threshold inside the CAD envelope, your main lever for shaving dead weight will be the separator housings of the arm gears (5010) and fingers (3205). Shifting those specific blocks from cast aluminum to high-grade carbon-fiber reinforced nylon (PA12-CF) 3D-prints will instantly shave roughly 1.5–2 kg of dead weight off the upper shoulder and hand assemblies.