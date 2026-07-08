# BB弾 弾道シミュレーター (BB-Ballistics)

An advanced 3D BB trajectory simulator for airsoft ballistics, based on modern fluid dynamics models including the Magnus effect and spin decay. 


## 🚀 Live Demo
*(Replace this with your GitHub Pages URL once hosted, e.g., `https://<your-username>.github.io/bb-ballistics/`)*

---

## 🌟 Features

* **Dual Drag Coefficient Models**: Toggle between the classic Morrison drag model ($C_d \approx 0.40$) and the modern Loth (2021) model ($C_d \approx 0.45$) for higher accuracy in airsoft speed ranges.
* **Intelligent Hop-Up Customization**:
  * **Auto (Optimal)**: Automatically calculates the maximum flat trajectory that doesn't over-hop more than 5mm from the line of sight.
  * **Zero-In (30m / 40m)**: Solves the exact backspin rate (rps) required to cross the line of sight at target distance.
  * **Manual Mode**: Manually adjust the backspin from 0 to 1,000 rotations per second.
* **Interactive 3D Viewport**: Powered by **Three.js** with multiple camera profiles (Chase Cam, Side Overview, and Free Orbit Cam) and playback speed controls (Real-time, 1/4× Slow-mo, 1/20× Super Slow-mo).
* **Comprehensive Metrics**: Outputs real-time velocity decay, muzzle/terminal energy (Joules), flight time, and a dynamic 2D graph with hover inspection.
* **Strict Japanese Regulations Check**: Visual safety badge indicating whether the muzzle energy stays within the legal limit of **0.98J**.

---

## 🔬 Mathematical & Physical Physics Model

This simulator tracks the 3D position vectors by numerically integrating the following differential equations (Runge-Kutta style discrete stepping):

### 1. Translational Acceleration
The acceleration vector $\vec{a}$ is derived from gravity, drag, and lift (Magnus force):

$$\vec{a} = \vec{g} - \frac{\rho A C_d |\vec{v}| \vec{v}}{2m} - \frac{k_{mag} (\vec{v} \times \vec{\omega})}{m}$$

Where:
* $m$ = Mass of the BB (kg)
* $\rho$ = Air density ($1.205 \text{ kg/m}^3$ at $20^\circ\text{C}$, 1 atm)
* $A$ = Cross-sectional area of the BB ($\pi R^2$)
* $C_d$ = Drag coefficient (Calculated via Morrison or Loth formulas based on the Reynolds number $Re$ and Mach number $Ma$)
* $k_{mag}$ = Magnus lift constant ($2 \rho C_l \frac{4}{3}\pi R^3$ where $C_l = 0.12$)

### 2. Rotational Decay (Spin-down)
The angular deceleration $\frac{d\omega}{dt}$ accounts for skin friction against the air:

$$\frac{d\omega}{dt} = -\frac{\rho R^4 C_f \cdot \frac{8\pi}{3} \sqrt{|\vec{v}|^2 + (c R |\vec{\omega}|)^2} \cdot \vec{\omega}}{2I}$$

Where:
* $I$ = Moment of inertia of a solid sphere ($\frac{2}{5}mR^2$)
* $C_f$ = Friction coefficient ($1.328 / \sqrt{Re}$)
* $c$ = Slip coefficient ($0.5$)

---

## 🛠️ Tech Stack

* **Frontend**: Vanilla HTML5, CSS3 (Modern dark UI, Flexbox/Grid)
* **Graphics**: Three.js (r128) via CDN
* **Computation**: Vanilla JavaScript (Numerical integration with $dt = 10^{-4}\text{ s}$)

---

## 📂 Installation & Usage

No build pipeline or server setup is required. It runs purely on the client side.

1. Clone this repository:
   ```bash
   git clone [https://github.com/your-username/bb-ballistics.git](https://github.com/your-username/bb-ballistics.git)