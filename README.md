# 🌀 Film-Cooling Database: Highly-Resolved LES of Jet-in-Crossflow Cooling

This repository hosts the **open-access database**:

> [https://github.com/uranos-gpu/film-cooling-database](https://github.com/uranos-gpu/film-cooling-database)

---

## 🧩 Overview

This database provides **highly-resolved Large-Eddy Simulation (LES)** data for a **canonical round-hole film-cooling configuration**, performed with the open-source GPU solver [**URANOS**](https://github.com/uranos-gpu/uranos-gpu).

The dataset explores the **combined effects of blowing ratio (M)** and **coolant-to-recovery temperature ratio (Tc/Tr)** on the **aerothermal behavior of transonic film-cooling jets**, establishing a modern reference for **model development**, **validation**, and **reduced-order analyses**.

Each simulation resolves the coupled dynamics of **momentum transport**, **thermal shielding**, and **wall-interacting vortices** that govern jet attachment, lift-off, and effectiveness decay.

---

## ⚙️ Simulation Matrix

| Parameter | Symbol | Values |
|:--|:--:|:--|
| Freestream Mach number | \( M_\infty \) | 0.8, 1.2, 1.6 |
| Coolant-to-recovery temperature ratio | \( T_c/T_r \) | 0.50, 0.75 |
| Wall condition | — | Adiabatic |
| Geometry | — | Flat plate, single round hole, 35° inclination |
| Domain extent | \( x^* = -40 \rightarrow 80 \), \( y/h = 15 \), \( z/h = 8 \) |
| Grid resolution | — | \( 2000 \times 384 \times 128 \) |
| LES model | — | Highly-resolved LES (WALE subgrid-scale closure) |
| Code | — | URANOS GPU-accelerated Navier–Stokes solver |

---

## 📂 Repository Organization

├── before-jet/                  # Upstream reference and inflow statistics
│   ├── mean-velocity
│   ├── mean-temperature
│   ├── velocity-fluctuations
│   └── temperature-fluctuations
│
├── after-jet/                   # Downstream (plume) region statistics
│   ├── velocity
│   ├── temperature
│   ├── reynolds-stress
│   ├── temperature-fluctuations
│   └── production-vs-diffusion
│
├── wall/                        # Near-wall and surface quantities
│   ├── adiabatic-effectiveness
│   ├── wall-temperature
│   ├── friction-coefficient
│   └── friction-reynolds
│
├── maxima/                      # Streamwise maxima of turbulent quantities
│   ├── max-tau11
│   └── max-trms
│
└── README.md

All data are stored as plain-text (`.txt`) tables with headers, readable with **NumPy**, **Matlab**, or **ParaView**.

---

## 📈 Quantities and Definitions

| Symbol | Description | Normalization |
|:--:|:--|:--|
| \( y^+ \) | Wall-normal coordinate | \( y u_\tau / \nu_w \) |
| \( u^+ \), \( u^+_{\mathrm{VD}} \) | Van-Driest–transformed velocity | \( \int_0^u \sqrt{\rho / \rho_w}\, du / u_\tau \) |
| \( T^* \) | Favre-averaged nondimensional temperature | \( \tilde{T}/T_\infty \) |
| \( \tau_{ij}^+ \) | Reynolds stresses | \( \tilde{u_i''u_j''} / u_\tau^2 \) |
| \( |P/\phi| \) | Production–diffusion balance | scaled by \( u_\tau^3 \rho_w / \delta_\nu \) |
| \( \eta \) | Adiabatic effectiveness | \( (T_r - T_w)/(T_r - T_c) \) |

---

## 🔬 Physical Insights

The simulations reveal:

- **Transition from buoyancy- to momentum-controlled regimes**:  
  For cold jets (\( T_c/T_r = 0.5 \)), the film remains attached and dense, suppressing wall shear.  
  For warm jets or high blowing ratios, lift-off occurs, dominated by jet momentum and entrainment.

- **Four-vortex topology** in the mean vorticity field:  
  A central counter-rotating vortex pair (CVP) drives inner/outer motion, while two wall-attached vortices laterally redistribute coolant, controlling wall coverage.

- **Spectral signatures**:  
  Transonic cases exhibit enhanced low-frequency content in wall-pressure spectra and an outer shear-layer energy ridge—trends consistent with increased jet penetration and unsteady lift-off.

These findings define a **transonic benchmark** for film cooling, bridging mean trends and spectral dynamics.

---

## 💾 Example Usage

### Python
```python
import numpy as np
yplus, cf = np.loadtxt("wall/friction-coefficient/M12_T05_cf.txt", unpack=True)

Matlab

data = readmatrix('wall/adiabatic-effectiveness/M16_T075_eta.txt');
yplus = data(:,1); eta = data(:,2);


⸻

📘 Citation

If you use this database, please cite:

⸻

🧠 Acknowledgments

Support from CINECA ISCRA Grants, NVIDIA, and the University of Padova – DII is gratefully acknowledged.

⸻

📄 License

Released under the MIT License.
Data may be used freely for academic and educational purposes with proper citation.

