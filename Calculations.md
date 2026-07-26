# Planar Mechanism (Elliptic Trammel) — Comprehensive Engineering Calculations

This document compiles the complete set of geometric, kinematic, dynamic, structural, tribological, and mechanical calculations for the **Planar Slider Mechanism** (Elliptic Trammel). 

---

## 1. Parameters & Dimensions from CAD Model

### A. Base Part (`BASE.PRT`)
* **Outer Square Envelope:** $250\text{ mm} \times 250\text{ mm}$
* **Base Extrusion Depth:** $100\text{ mm}$ (Symmetric extrusion)
* **Orthogonal Guidance Slots Width:** $50\text{ mm}$
* **Slot Material Removal Depth:** $50\text{ mm}$
* **Base Outer Corner Chamfers:** $20\text{ mm} \times 45^\circ$ on all 4 vertical edges

### B. Connector Link (`CONNECTOR.PRT`)
* **Center-to-Center Distance ($L$):** $100\text{ mm}$ (between pin hole centers)
* **Reamed Joint Pin Holes:** $\varnothing 20\text{ mm}$ (2 holes)
* **End Boss Outer Radius / Diameter:** $R25\text{ mm} \rightarrow \varnothing 50\text{ mm}$
* **Link Width:** $30\text{ mm}$
* **Extrusion Thickness:** $15\text{ mm}$

### C. Pin / Slider Block (`PIN.PRT`)
* **Slider Block Base Dimensions:** $50\text{ mm (width)} \times 70\text{ mm (length)}$
* **Slider Block Height:** $50\text{ mm}$ (Symmetric extrusion)
* **Upright Cylindrical Pin Diameter:** $\varnothing 20\text{ mm}$
* **Upright Pin Height:** $30\text{ mm}$

### D. Kinematic Input Parameters
* **Servo Motor Input:** Rotational Motion / Angular Velocity ($\omega$)
* **Angular Velocity Magnitude:** $\omega = 10^\circ/\text{sec} = 0.17453\text{ rad/sec}$
* **Simulation Duration:** $t = 500\text{ seconds}$

---

## 2. Mobility & Degree of Freedom (Grübler's Equation)

For a 2D planar mechanism:

$$F = 3(n - 1) - 2j_1 - j_2$$

* **Number of Links ($n$):** 4
  * $N_1$: Fixed Base Plate (Ground)
  * $N_2$: Slider Block 1 ($X$-axis)
  * $N_3$: Slider Block 2 ($Y$-axis)
  * $N_4$: Connector Link
* **Lower Pairs / 1-DOF Joints ($j_1$):** 4
  * 2 Prismatic sliding joints (Slider 1 in Slot 1, Slider 2 in Slot 2)
  * 2 Revolute pin joints (Slider 1 to Link, Slider 2 to Link)
* **Higher Pairs / 2-DOF Joints ($j_2$):** 0

$$F = 3(4 - 1) - 2(4) - 0 = 9 - 8 = 1\text{ Degree of Freedom}$$

> **Conclusion:** The system possesses **1 Degree of Freedom**, ensuring deterministic, fully constrained kinematic motion.

---

## 3. Kinematic Trajectory Equations

With the guideway channels oriented along orthogonal $X$ and $Y$ axes:

### A. Position Functions of Sliders
* **Slider 1 Position ($X$-axis):**
  $$x_1(\theta) = L \cdot \cos(\theta) = 100 \cdot \cos(\theta)\text{ [mm]}$$

* **Slider 2 Position ($Y$-axis):**
  $$y_2(\theta) = L \cdot \sin(\theta) = 100 \cdot \sin(\theta)\text{ [mm]}$$

### B. Trajectory of Any Arbitrary Point $P(d)$ along Connector Link
For a point $P$ located at distance $d$ from Slider 1:

$$x_P(\theta) = (L - d) \cdot \cos(\theta)$$
$$y_P(\theta) = d \cdot \sin(\theta)$$

Eliminating $\theta$ via $\cos^2(\theta) + \sin^2(\theta) = 1$:

$$\left(\frac{x_P}{L - d}\right)^2 + \left(\frac{y_P}{d}\right)^2 = 1$$

* **Midpoint ($d = 50\text{ mm}$):**
  $$\left(\frac{x_P}{50}\right)^2 + \left(\frac{y_P}{50}\right)^2 = 1 \implies x_P^2 + y_P^2 = 50^2$$
  *Traces a **perfect circle** of radius $R = 50\text{ mm}$.*

* **General Point ($d \neq 50\text{ mm}$):**
  *Traces a true **ellipse** with semi-major axis $a = \max(d, L-d)$ and semi-minor axis $b = \min(d, L-d)$.*

---

## 4. Velocity & Acceleration Analysis

For input speed $\omega = 0.17453\text{ rad/sec}$:

### A. Linear Velocities
$$v_{x1}(\theta) = \frac{dx_1}{dt} = -L \omega \sin(\theta) = -17.453 \sin(\theta)\text{ mm/sec}$$
$$v_{y2}(\theta) = \frac{dy_2}{dt} = L \omega \cos(\theta) = 17.453 \cos(\theta)\text{ mm/sec}$$

* **Peak Slider Velocity:**
  $$v_{\max} = L \cdot \omega = 100\text{ mm} \times 0.17453\text{ rad/s} = 17.453\text{ mm/s} = 0.01745\text{ m/s}$$

### B. Linear Accelerations
$$a_{x1}(\theta) = \frac{d^2 x_1}{dt^2} = -L \omega^2 \cos(\theta) = -3.046 \cos(\theta)\text{ mm/sec}^2$$
$$a_{y2}(\theta) = \frac{d^2 y_2}{dt^2} = -L \omega^2 \sin(\theta) = -3.046 \sin(\theta)\text{ mm/sec}^2$$

* **Peak Slider Acceleration:**
  $$a_{\max} = L \cdot \omega^2 = 100\text{ mm} \times (0.17453\text{ rad/s})^2 = 3.046\text{ mm/s}^2 = 0.00305\text{ m/s}^2$$

---

## 5. Mechanical Advantage & Force Transmission

Using virtual work principles for ideal power transfer ($P_{\text{in}} = P_{\text{out}}$):

$$\omega \cdot T_d = v_x \cdot F_x + v_y \cdot F_y$$

### A. Required Transmitted Forces
* **Force at Slider 1 ($X$-axis):**
  $$F_x(\theta) = -\frac{T_d}{100 \cdot \sin(\theta)}$$

* **Force at Slider 2 ($Y$-axis):**
  $$F_y(\theta) = \frac{T_d}{100 \cdot \cos(\theta)}$$

### B. Singularity Analysis
* **At $\theta = 0^\circ, 180^\circ$:** $\sin(\theta) = 0 \implies F_x \to \infty$ (Slider 1 reaches extreme stroke; mechanical toggle/dead-center position).
* **At $\theta = 90^\circ, 270^\circ$:** $\cos(\theta) = 0 \implies F_y \to \infty$ (Slider 2 reaches extreme stroke).

---

## 6. Friction Constraints & Anti-Binding Condition

### Anti-Jamming Aspect Ratio Rule
To prevent tilting and mechanical self-locking of the slider inside the $50\text{ mm}$ slot guideway:

$$\frac{L_{\text{slider}}}{W_{\text{slider}}} > 2 \mu$$

Where:
* Slider Length ($L_{\text{slider}}$) = $70\text{ mm}$
* Slider Width ($W_{\text{slider}}$) = $50\text{ mm}$
* Friction coefficient (unlubricated metal) $\mu \approx 0.15$

$$\frac{70}{50} = 1.40$$
$$2\mu = 2 \times 0.15 = 0.30$$

Since **$1.40 > 0.30$**, smooth non-binding motion is guaranteed.

---

## 7. Stress & Structural Analysis on Pin Joint

Evaluating peak stress for an assumed maximum load $F_{\max} = 500\text{ N}$ on the $\varnothing 20\text{ mm}$ upright pin ($h = 30\text{ mm}$):

### A. Direct Shear Stress ($\tau$)
$$A_{\text{pin}} = \frac{\pi}{4} d^2 = \frac{\pi}{4} (20)^2 = 314.16\text{ mm}^2$$
$$\tau = \frac{F_{\max}}{A_{\text{pin}}} = \frac{500\text{ N}}{314.16\text{ mm}^2} = 1.59\text{ MPa}$$

### B. Maximum Bending Stress ($\sigma_b$)
Applied load moment arm $h_{\text{arm}} = 22.5\text{ mm}$:

$$M_b = 500\text{ N} \times 22.5\text{ mm} = 11,250\text{ N}\cdot\text{mm}$$
$$Z = \frac{\pi d^3}{32} = \frac{\pi (20)^3}{32} = 785.40\text{ mm}^3$$
$$\sigma_b = \frac{M_b}{Z} = \frac{11,250}{785.40} = 14.32\text{ MPa}$$

### C. Von Mises Equivalent Combined Stress ($\sigma_{\text{vm}}$)
$$\sigma_{\text{vm}} = \sqrt{\sigma_b^2 + 3\tau^2} = \sqrt{(14.32)^2 + 3(1.59)^2} = 14.58\text{ MPa}$$

> **Assessment:** Peak stress ($14.58\text{ MPa}$) provides a generous safety factor ($SF \approx 18.8$) against yielding for Al 6061-T6 ($S_y = 275\text{ MPa}$).

---

## 8. Dynamic Inertia & Kinetic Energy

### A. Component Masses
* **Connector Link Mass ($m_c$, Al 6061, $\rho = 2700\text{ kg/m}^3$):**  
  $$V_c = 72,000\text{ mm}^3 = 7.2 \times 10^{-5}\text{ m}^3 \implies m_c = 0.1944\text{ kg}$$
* **Slider Block Mass ($m_s$, SAE 660 Bronze, $\rho = 8800\text{ kg/m}^3$):**  
  $$V_s = 184,425\text{ mm}^3 = 1.844 \times 10^{-4}\text{ m}^3 \implies m_s = 1.623\text{ kg}$$

### B. Total System Kinetic Energy
$$E_k(\theta) = \frac{1}{2} m_s v_{x1}^2 + \frac{1}{2} m_s v_{y2}^2 + \frac{1}{2} I_{zz} \omega^2$$
$$E_k = \frac{1}{2} m_s L^2 \omega^2 (\sin^2\theta + \cos^2\theta) + \frac{1}{2} I_{zz} \omega^2 = \frac{1}{2} \left( m_s L^2 + I_{zz} \right) \omega^2$$

> **Key Insight:** Total dynamic kinetic energy is **constant** over time for constant $\omega$, meaning zero net dynamic torque is required to sustain rotation in the absence of friction.

---

## 9. Tribological Friction & Wear Analysis

### A. Average Friction Power Loss
For vertical weight load $W_s = m_s g = 1.623 \times 9.81 = 15.92\text{ N}$ per slider and $\mu = 0.15$:

$$F_{\text{friction}} = \mu \cdot W_s = 0.15 \times 15.92\text{ N} = 2.388\text{ N}$$
$$v_{\text{avg}} = \frac{2}{\pi} v_{\max} = 11.11\text{ mm/s} = 0.01111\text{ m/s}$$
$$P_{\text{loss, total}} = 2 \times (F_{\text{friction}} \cdot v_{\text{avg}}) = 2 \times (2.388 \times 0.01111) = 0.053\text{ W} = 53\text{ mW}$$

### B. Archard's Wear Volume Rate ($Q$)
For $t = 500\text{ s}$ runtime (total sliding distance $S = v_{\text{avg}} \cdot t = 5.555\text{ m}$):

$$Q = K \cdot \frac{W_s \cdot S}{H} = (1 \times 10^{-4}) \cdot \frac{15.92\text{ N} \times 5.555\text{ m}}{8.5 \times 10^8\text{ N/m}^2} = 0.0104\text{ mm}^3$$

---

## 10. Hertzian Contact Stress (Pin-Hole Joint)

For $\varnothing 20.00\text{ mm}$ pin in $\varnothing 20.05\text{ mm}$ hole under $F = 500\text{ N}$ joint load:

$$p_{\max} = \sqrt{\frac{F \cdot E^*}{\pi \cdot L_{\text{contact}} \cdot R^*}} = \sqrt{\frac{500 \times (50 \times 10^3)}{\pi \times 15 \times 4010}} \approx 11.5\text{ MPa}$$

> **Conclusion:** Peak Hertzian pressure ($11.5\text{ MPa}$) is comfortably below the surface yield limits of Bronze ($125\text{ MPa}$) and Aluminum ($275\text{ MPa}$), ensuring long fatigue life without surface pitting