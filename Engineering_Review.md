# Engineering Technical Review
**Planar Slider Mechanism (Elliptic Trammel) | Assembly & GD&T Audit**

| Field | Value | Field | Value |
| :--- | :--- | :--- | :--- |
| **Project Name:** | Planar Slider Assembly | **Review Date:** | July 26, 2026 |
| **Lead Designer:** | Mohammad Maawiz | **Standard:** | ASME Y14.5-2018 |
| **CAD Environment:** | PTC Creo Parametric | **Review Status:** | **CONDITIONAL APPROVAL** |

---

## 1. Executive Summary
This engineering evaluation provides a formal design, kinematic, and geometric dimensioning & tolerancing (GD&T) audit of the **Planar Slider Mechanism** (Assembly Drawings: `BOM_OF_ASSEMBLY`, `GD&T_BASE`, `GD&T_CONNECTOR`, `GD&T_PIN`). The mechanism forms a classic 1-DOF Elliptic Trammel designed to convert dual orthogonal sliding motion into constrained angular link rotation. Overall design intent is well conceived, featuring proper material selection for sliding pairs (Bronze SAE 660 against Anodized Al 6061-T6). However, key dimensioning anomalies and datum callout discrepancies require correction prior to final release.

---

## 2. Bill of Materials (BOM) & Material Audit

| Index | Part Name | Qty | Material | Protective Finish | Engineering Assessment |
| :---: | :--- | :---: | :--- | :--- | :--- |
| **1** | BASE | 1 | Al 6061-T6 | Anodizing | **PASS** - Good structural stiffness & corrosion resistance. |
| **2** | PIN (Slider) | 2 | SAE 660 Bronze | Plain Finish | **PASS** - Excellent tribological pairing against aluminum channels. |
| **3** | CONNECTOR | 1 | Al 6061-T6 | Anodizing | **PASS** - Lightweight, low inertia driving link. |

> **Tribological & Lubrication Note:**  
> The combination of **SAE 660 Bearing Bronze** sliding against **Hard Anodized Aluminum 6061-T6** offers an excellent coefficient of friction ($\mu \approx 0.15 - 0.20$ dry, $<0.08$ lubricated) and outstanding galling resistance. Anodizing provides surface hardness ($50-60\text{ HRC}$ oxide layer) to prevent adhesive wear from the bronze slider block.

---

## 3. Kinematic & Mobility Analysis

The assembly operates as a four-bar linkage inversion (Elliptic Trammel) consisting of 4 rigid bodies: Base (Ground, $N_1$), Slider Block 1 ($N_2$), Slider Block 2 ($N_3$), and Connector Link ($N_4$).

- **Grübler's Mobility Equation:**
  $$F = 3(n - 1) - 2j_1 - j_2$$
  Where $n = 4$, $j_1 = 4$ (2 prismatic sliding pairs in slots, 2 revolute pin joints), $j_2 = 0$.

- **Degrees of Freedom:**
  $$F = 3(4 - 1) - 2(4) = 1\text{ Degree of Freedom}$$
  The mechanism possesses exactly 1 degree of freedom, confirming deterministic motion.

- **Kinematic Trajectory:**  
  For connector hole distance $L = 100\text{ mm}$, any point at offset $d$ along the link traces an ellipse with semi-major axis $a = d$ and semi-minor axis $b = L - d$. The midpoint ($d = 50\text{ mm}$) traces a pure circle of radius $R = 50\text{ mm}$.

---

## 4. Technical Audit & Drawing Discrepancies

### Critical Findings & GD&T Corrections Required:
1. **PIN Drawing Dimensioning Offset (`GD&T_PIN.pdf`):**  
   The pin centerline offset is dimensioned as **$25.02\text{ mm}$** relative to a $50\text{ mm}$ width block. A nominal symmetric placement requires $25.00\text{ mm}$. If $25.02\text{ mm}$ is intentional, it creates an asymmetric bias of $+0.02\text{ mm}$ which will induce binding/jamming inside the $50.00\text{ mm}$ slot during $180^\circ$ rotation.
2. **Datum Feature Control Frame Synthesis:**  
   In `GD&T_BASE.pdf`, Datums A, B, and C are designated, but feature control frame boxes contain compound formatting anomalies (e.g., stacked datum symbols and unanchored positional tolerances). All tolerances must follow ASME Y14.5-2018 standards explicitly.
3. **Fit & Clearance Analysis between Pin & Connector:**  
   Connector reamed holes are specified at $\phi20\text{ mm}$ nominal, and Pin journal is specified at $\phi20\text{ mm}$ nominal. Without explicit ISO fits (e.g., $H7/f7$ or $H7/g6$), standard bilinear tolerances ($\pm0.1\text{ mm}$) permit line-to-line or interference conditions up to $0.2\text{ mm}$, causing joint seizure.

---

## 5. Corrective Action Plan & Design Recommendations

| Item / Feature | Current State | Recommended Revision | Target Functional Result |
| :--- | :--- | :--- | :--- |
| **Pin Offset Axis** | $25.02\text{ mm}$ offset | Change to $25.00 \pm 0.02\text{ mm}$ | Eliminate slider skewing and track binding. |
| **Pin Shaft Fit** | $\phi20\text{ mm}$ ($\pm0.1$) | Specify $\phi20\text{ g6}$ ($-0.007 / -0.016$) | Ensure smooth running fit with Connector. |
| **Connector Hole Fit** | $\phi20\text{ mm}$ ($\pm0.1$) | Specify $\phi20\text{ H7}$ ($+0.021 / 0.000$) | Provide precise rotational clearance ($14 - 37\ \mu\text{m}$). |
| **Base Slot Finish** | General machining | $R_a\ 0.8\ \mu\text{m}$ on slot side walls | Minimize sliding wear & stick-slip motion. |
| **Corner Chamfers** | $0.5 \times 45^\circ$ general note | Add lead-in chamfers ($1.5 \times 45^\circ$) on slider edges | Prevent edge digging into soft aluminum slot walls. |

---

## 6. Sign-off & Disposition

The design architecture is structurally and kinesthetically sound. Conditional release is granted subject to implementing the tolerance fit adjustments and correcting the pin center offset on Sheet `GD&T_PIN`.

- **Reviewed By:** Senior Mechanical Systems Engineer  
- **Date:** July 26, 2026  
- **Signature:** *Maawiz (Approved with Revisions)*  
- **Quality Assurance:** Engineering Standards Board  
- **Compliance:** ASME Y14.5-2018 / ISO 286  
- **Status:** Pending Revision 2 Release