# Open-Humanoid-180 – Kinematic Scheme

## General Specifications
- **Height:** 180 cm
- **Weight:** ~55 kg
- **Total Degrees of Freedom (DoF):** 36
- **Actuators:** 36 (one BLDC motor per DoF)
- **Motor types:**
  - High‑power: 6384 120KV – 6 units
  - Medium: 5065 140KV – 7 units
  - Basic: 5010 360KV – 10 units
  - Low‑power: 3205 110KV – 13 units
- **Gearboxes:** Harmonic (or cycloidal) drives with reduction ratios:
  - 1:100 – for high‑power motors
  - 1:65 – for medium motors and basic motors in the hip
  - 1:40 – for low‑power motors and basic motors in shoulders, elbows and wrists

---

## Joint Distribution

### Lower Limbs – 8 DoF (6 high‑power + 2 basic)

| Joint | DoF | Motor Type |
|-------|-----|------------|
| Left hip | 3 (flexion‑extension, abduction‑adduction, rotation) | 2 high‑power + 1 basic |
| Right hip | 3 (flexion‑extension, abduction‑adduction, rotation) | 2 high‑power + 1 basic |
| Left knee | 1 (flexion‑extension) | 1 high‑power |
| Right knee | 1 (flexion‑extension) | 1 high‑power |

> **Note:** Feet are passive rounded cylinders with no moving joints.

---

### Torso – 4 DoF (1 medium + 3 low‑power)

| Joint | DoF | Motor Type |
|-------|-----|------------|
| Lumbar (waist) | 1 (forward‑backward tilt) | 1 medium |
| Neck | 3 (tilt, pan, roll) | 3 low‑power |

---

### Upper Limbs – 24 DoF (6 medium + 8 basic + 10 low‑power)

| Joint | DoF | Motor Type |
|-------|-----|------------|
| Left shoulder | 3 (elevation, abduction, rotation) | 2 medium + 1 basic |
| Right shoulder | 3 (elevation, abduction, rotation) | 2 medium + 1 basic |
| Left elbow | 2 (flexion‑extension + forearm rotation) | 1 medium + 1 basic |
| Right elbow | 2 (flexion‑extension + forearm rotation) | 1 medium + 1 basic |
| Left wrist | 2 (flexion‑extension, abduction‑adduction) | 2 basic |
| Right wrist | 2 (flexion‑extension, abduction‑adduction) | 2 basic |
| Left fingers (5) | 1 per finger (flexion) | 5 low‑power |
| Right fingers (5) | 1 per finger (flexion) | 5 low‑power |

> **Note:** Each finger has a single actuator providing basic grasping capability. Full anatomical articulation is not reproduced.

---

## Motor Summary

| Type | Quantity | Location |
|------|----------|----------|
| 6384 120KV (high‑power) | 6 | Hips (4) + knees (2) |
| 5065 140KV (medium) | 7 | Waist (1), shoulders (4), elbows (2) |
| 5010 360KV (basic) | 10 | Hips (2), shoulders (2), elbows (2), wrists (4) |
| 3205 110KV (low‑power) | 13 | Neck (3) + fingers (10) |

---

## Actuator Control
- **High‑power motors** are driven by **ODrive 3.6** controllers.
- **Medium and basic motors** are driven by **hoverboard mainboards** (running *hoverboard‑firmware‑hack‑FOC*).
- **Low‑power motors** use **SimpleFOCMini** boards (based on AT32F403ACGU7, with MS8313 driver).
- **Encoders:** All motors are equipped with **MT6826S** absolute magnetic encoders.
- **Central processing:** ESP32‑S3 acts as a gateway, while a laptop with an RTX 3080 handles high‑level computation.

---

## Power Supply
- **Battery:** 7S Li‑NMC (25.9–29.4 V), with a 200 A BMS.
- **Power distribution:** via DC‑DC converters and protective circuit breakers.