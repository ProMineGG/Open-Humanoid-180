# Actuator Calculations — Open-Humanoid-180

> **Status:** work in progress.
>
> This document will contain the complete actuator system calculations for the robot.

## Planned Content

- KV selection for each motor type (6384, 5065, 3205) with justification.
- Torque calculations for each joint, based on the robot's estimated weight (~50 kg).
- Required reduction ratios for high‑torque (1:100), medium (1:65), and base (1:40) joints.
- Current margin verification for selected drivers (ODrive, hoverboard ESCs, SimpleFOCMini).
- Peak and continuous load estimates for walking gait.

## When It Will Be Completed

This document will be finalized after:
1. Full CAD model of the robot is built.
2. Kinematics and dynamics calculations are completed in Gazebo or MATLAB.
3. First joint prototype is tested on a bench.

---

*Available now: [BOM.en.md](BOM.en.md), [power_schematic.en.md](power_schematic.en.md), [weight_budget.en.md](weight_budget.en.md)*