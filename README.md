# Elliptic Trammel / Planar Slider Mechanism

## Project Overview
This repository contains the complete design, Bill of Materials (BOM), and Geometric Dimensioning and Tolerancing (GD&T) documentation for a **Planar Slider Mechanism** (commonly known as an *Elliptic Trammel* or *Trammel of Archimedes*). 

The mechanism translates rotary/angular motion into linear orthogonal sliding motion, consisting of a slotted base plate, two sliding pin blocks, and a connecting link.

---

## File Structure & Assembly Components

### Assembly Components
1. **BASE** (`BASE1.PRT`)
   - **Quantity:** 1
   - **Material:** Aluminum 6061-T6
   - **Finish:** Anodized
   - **Function:** Provides perpendicular guideways (50 mm width) for orthogonal motion constrained in two axes.
2. **PIN / SLIDER BLOCK** (`PIN.PRT`)
   - **Quantity:** 2
   - **Material:** SAE 660 Bearing Bronze (Cast Bronze)
   - **Finish:** Plain Finish
   - **Function:** Slider block (50 x 50 x 70 mm) with a cylindrical pin (Ø20 mm) engaging with the connector link.
3. **CONNECTOR** (`CONNECTOR.PRT`)
   - **Quantity:** 1
   - **Material:** Aluminum 6061-T6
   - **Finish:** Anodized
   - **Function:** Links both pin sliders with 100 mm center-to-center distance (Ø20 mm reamed holes), dictating the elliptical path tracing.

---

## Kinematic Summary
- **Mechanism Type:** Planar 1-DOF Slider-Crank / Elliptic Trammel inversion.
- **Grashof / Mobility Condition:** $F = 3(n - 1) - 2j_1 - j_2 = 3(4 - 1) - 2(4) - 0 = 1\text{ Degree of Freedom}$.
- **Motion Characteristics:** Midpoint of the connector traces a perfect circle, while all other points on the connector line trace exact ellipses.

---

## Documentation Files
- `BOM_OF_ASSEMBLY.pdf`: Assembly view & Bill of Materials drawing.
- `GD&T_BASE.pdf`: Detailed manufacturing & GD&T drawing for the slotted Base.
- `GD&T_CONNECTOR.pdf`: Detailed manufacturing & GD&T drawing for the Connector link.
- `GD&T_PIN.pdf`: Detailed manufacturing & GD&T drawing for the Pin Sliders.
- `Planar_Mechanism-Gif.gif`: Kinematic animation of the assembly in Creo Parametric.
- `Engineering_Review.md`: Comprehensive Design & Engineering Review report in Markdown.
- `Calculations.md`: Engineering Calculations.

---

## Author & Engineering Information
- **Drawn By:** Mohammad Maawiz
- **Date:** July 26, 2026
- **Standard:** ASME Y14.5-2018
