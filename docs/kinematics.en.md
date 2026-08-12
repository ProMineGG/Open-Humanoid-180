# Kinematic Scheme of Open-Humanoid-180

## General Parameters
- **Height:** 180 cm
- **Weight:** ~55 kg
- **Total Degrees of Freedom (DoF):** 36
- **Number of actuators:** 36 (each DoF is driven by a separate BLDC motor)
- **Motor types:**
  - High-power (6384 120KV) – 6 pcs.
  - Medium (5065 140KV) – 17 pcs.
  - Basic (3205 110KV) – 13 pcs.
- **Gearboxes:** harmonic (or cycloidal) drives with ratios:
  - 1:100 – for high-power
  - 1:65 – for medium
  - 1:40 – for basic

## Joint Distribution

### Lower Limbs – 8 DoF (6 high-power + 2 medium)
| Joint | DoF | Motor type |
|-------|-----|------------|
| Left hip | 3 (flexion/extension, abduction/adduction, rotation) | 2 high + 1 medium |
| Right hip | 3 (flexion/extension, abduction/adduction, rotation) | 2 high + 1 medium |
| Left knee | 1 (flexion/extension) | 1 high |
| Right knee | 1 (flexion/extension) | 1 high |

> **Note:** Feet are passive rounded cylinders with no actuated joints.

### Torso – 4 DoF (1 medium + 3 basic)
| Joint | DoF | Motor type |
|-------|-----|------------|
| Waist (lumbar) | 1 (forward/backward tilt) | 1 medium |
| Neck | 3 (tilt, pan, roll) | 3 basic |

### Upper Limbs – 24 DoF (14 medium + 10 basic)
| Joint | DoF | Motor type |
|-------|-----|------------|
| Left shoulder | 3 (elevation, abduction, rotation) | 3 medium |
| Right shoulder | 3 (elevation, abduction, rotation) | 3 medium |
| Left elbow | 2 (flexion/extension + forearm rotation) | 2 medium |
| Right elbow | 2 (flexion/extension + forearm rotation) | 2 medium |
| Left wrist | 2 (flexion/extension, abduction/adduction) | 2 medium |
| Right wrist | 2 (flexion/extension, abduction/adduction) | 2 medium |
| Left fingers (5) | 1 each (flexion) | 5 basic |
| Right fingers (5) | 1 each (flexion) | 5 basic |

> **Note:** Each finger has a single actuator to enable basic grasping, not full anatomical dexterity.

## Motor Type Summary

| Type | Quantity | Usage |
|------|----------|-------|
| 6384 120KV (high) | 6 | Hips (4) + knees (2) |
| 5065 140KV (medium) | 17 | Hip rotation (2), waist (1), shoulders (6), elbows (4), wrists (4) |
| 3205 110KV (basic) | 13 | Neck (3) + fingers (10) |

### Actuator Control
- **High‑power and medium motors** are driven by **ODrive 3.6** controllers or **hoverboard mainboards** (running *hoverboard‑firmware‑hack‑FOC*) – both with **MT6826S** absolute encoders.
- **Basic motors** use **SimpleFOCMini** boards (based on AT32F403ACGU7, with MS8313 driver) – also equipped with MT6826S encoders.
- **Central processing:** ESP32‑S3 acts as a gateway, while a laptop with an RTX 3080 handles high‑level computation.

## Power
- 7S Li‑NMC battery (25.9–29.4 V), BMS rated at 200A.
- Power distribution via DC‑DC converters and protective circuit breakers.