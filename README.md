# 🌀 Film-Cooling Database: Highly-Resolved LES of Jet-in-Crossflow Cooling

This repository hosts the **open-access database**:  
👉 [https://github.com/uranos-gpu/film-cooling-database](https://github.com/uranos-gpu/film-cooling-database)

---

## 🧩 Overview

This database provides **highly-resolved Large-Eddy Simulation (LES)** data for a **canonical round-hole film-cooling configuration**, performed with the open-source GPU solver [**URANOS**](https://github.com/uranos-gpu/uranos-gpu).

The dataset explores the **combined effects of blowing ratio** (<span>$M$</span>) and **coolant-to-recovery temperature ratio** (<span>$T_c/T_r$</span>) on the **aerothermal behavior of transonic film-cooling jets**, establishing a modern reference for **model development**, **validation**, and **reduced-order analyses**.

Each simulation resolves the coupled dynamics of **momentum transport**, **thermal shielding**, and **wall-interacting vortices** that govern jet attachment, lift-off, and effectiveness decay.

---

## ⚙️ Simulation Matrix

| Parameter | Symbol | Values |
|:--|:--:|:--|
| Freestream Mach number | <span>$M_\infty$</span> | 0.8, 1.2, 1.6 |
| Coolant-to-recovery temperature ratio | <span>$T_c/T_r$</span> | 0.50, 0.75 |
| Wall condition | — | Adiabatic |
| Geometry | — | Flat plate, single round hole, 30° inclination |
| Domain extent | <span>$x/$</span>, <span>$y$</span>, <span>$z$</span> | 50:100, 0:20, -5:5
| Grid resolution | — | <span>$2000 \times 384 \times 128$</span> |
| LES model | — | Highly-resolved LES (WALE subgrid-scale closure) |
| Solver | — | URANOS GPU-accelerated Navier–Stokes solver |

---

All data are stored as plain-text (`.txt`) tables with headers, directly readable with **NumPy**, **Matlab**, or **ParaView**.

---

## 📈 Quantities and Definitions

| Symbol | Description | Normalization |
|:--:|:--|:--|
| <span>$y^+$</span> | Wall-normal coordinate | <span>$y u_\tau / \nu_w$</span> |
| <span>$u^+$</span>, <span>$u^+_{\mathrm{VD}}$</span> | Van-Driest–transformed velocity | <span>$\int_0^u \sqrt{\rho / \rho_w}\, du / u_\tau$</span> |
| <span>$T^*$</span> | Favre-averaged nondimensional temperature | <span>$\tilde{T}/T_\infty$</span> |
| <span>$\tau_{ij}^+$</span> | Reynolds stresses | <span>$(\rho/\rho_w) \widetilde{u_i''u_j''}/u_\tau^2$</span> |
| <span>$P|\phi$</span> | Production–diffusion balance | scaled by <span>$u_\tau^3 \rho_w / \delta_\nu$</span> |
| <span>$\eta$</span> | Adiabatic effectiveness | <span>$(T_r - T_w)/(T_r - T_c)$</span> |

---

## 🔬 Physical Insights

- **Transition from buoyancy- to momentum-controlled regimes**  
  Cold jets (<span>$T_c/T_r = 0.5$</span>) remain attached and dense, reducing wall shear.  
  Warm jets or high blowing ratios lift off, dominated by jet momentum and entrainment.

- **Four-vortex topology in mean vorticity**  
  A counter-rotating vortex pair (CVP) governs vertical and lateral entrainment, while two wall-attached vortices redistribute coolant near the surface, controlling wall coverage.

- **Spectral behavior**  
  Transonic regimes exhibit strong low-frequency oscillations in wall-pressure spectra and enhanced shear-layer energy ridges, characteristic of periodic jet lift-off and reattachment.

These findings provide a **benchmark for transonic film-cooling flows**, linking wall protection, jet entrainment, and turbulence structure.

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
Data may be freely used for academic and educational purposes with proper citation.

