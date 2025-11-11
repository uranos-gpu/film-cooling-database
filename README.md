# Film-Cooling Database for Scale-Resolved Simulations

Comprehensive dataset of **highly-resolved LES** film-cooling simulations generated with the open-source solver [URANOS](https://github.com/uranos-gpu/uranos-gpu).  
The database includes pre-processed mean and fluctuating quantities, Reynolds stresses, and transport-term budgets for multiple blowing ratios and coolant-to-mainstream temperature ratios.

---

## Repository Structure

All simulation outputs are organized by *region* and *physical quantity*, ensuring consistent naming and easy access for analysis and model validation.

├── before-jet/                  # Upstream (inflow) region statistics
│   ├── mean-velocity
│   ├── mean-temperature
│   ├── velocity-fluctuations
│   └── temp-fluctuations
│
├── after-jet/                   # Downstream (plume / recovery) region statistics
│   ├── velocity
│   ├── temperature
│   ├── reynolds-stress
│   ├── temp-fluctuations
│   └── production-vs-diffusion
│
├── wall/                        # Near-wall quantities and effectiveness
│   ├── adiabatic-effectiveness
│   ├── wall-temperature
│   ├── cf
│   └── friction-reynolds
│
├── maxima/                      # Streamwise maxima of turbulence statistics
│   ├── max-tau11
│   └── max-trms
│
└── README.md

Each subdirectory contains plain-text (`.txt`) profiles with column headers, ready for direct loading in **Python**, **Matlab**, or **ParaView**.

---

## Quantities and Definitions

| Symbol | Description | Normalization |
|:--:|:--|:--|
| \( y^+ \) | Wall-normal coordinate | \( y u_\tau / \nu_w \) |
| \( u^+ \), \( u^+_{\mathrm{VD}} \) | Van Driest–transformed velocity | \( \int_0^u \sqrt{\rho / \rho_w}\, du / u_\tau \) |
| \( T^* \) | Favre-averaged nondimensional temperature | \( \tilde T / T_\infty \) |
| \( T_{\mathrm{rms}}^+ \) | Temperature fluctuations | \( T_{\mathrm{rms}} / u_\tau^2 \) |
| \( \tau_{ij}^+ \) | Reynolds stress tensor components | \( (\rho/\rho_w)\, \widetilde{u_i''u_j''}/u_\tau^2 \) |
| \( |P/\phi| \) | Production–diffusion balance | scaled by \( u_\tau^3 \rho_w / \delta_\nu \) |
| \( \eta \) | Adiabatic effectiveness | \( (T_r - T_w)/(T_r - T_c) \) |

---

## Simulation Parameters

| Parameter | Symbol | Values |
|:--|:--:|:--|
| Freestream Mach number | \( M_\infty \) | 0.8, 1.2, 1.6 |
| Coolant-to-mainstream temperature ratio | \( T_c / T_r \) | 0.50, 0.75 |
| Wall condition | — | adiabatic |
| Jet geometry | — | round hole, 35° inclination |
| Solver | — | [URANOS GPU-accelerated Navier–Stokes solver](https://github.com/uranos-gpu/uranos-gpu) |
| LES model | — | Highly-resolved LES with equilibrium wall law |
| Grid size | — | 2000 × 384 × 128 |
| Domain extent | — | \( x^* = -40 \) → \( 80 \) |

---

## File Format and Usage

All datasets are plain ASCII text with headers:

```text
# Columns: yplus  tau11_plus  case=M08_T05  x*=10.0
0.5   0.12
1.0   0.25
...

Load Example (Python)

import numpy as np
yplus, tau11p = np.loadtxt("after-jet/reynolds-stress/M08_T05_tau11.txt", unpack=True)

Load Example (Matlab)

data = readmatrix('wall/adiabatic-effectiveness/M08_T05_eta.txt');
yplus = data(:,1); eta = data(:,2);


⸻

How to Cite


⸻

Related Work
	•	URANOS Solver￼

⸻

Maintainer

Francesco De Vanna
Assistant Professor – Machine Fluid Dynamics
University of Padova, Department of Industrial Engineering￼
📧 francesco.devanna@unipd.it

⸻

License

This repository is released under the MIT License.
Data may be freely used for academic and educational purposes with proper citation.

⸻

Acknowledgments

Support from CINECA ISCRA Grants, NVIDIA, and the University of Padova – DII is gratefully acknowledged.


