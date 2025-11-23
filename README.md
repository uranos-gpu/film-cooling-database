# 📘 Film-Cooling Database — High-Fidelity LES (URANOS-GPU)

This repository provides an **open-access database** of high-fidelity **Large-Eddy Simulations (LES)** for a **canonical round-hole film-cooling jet in crossflow**, performed using **URANOS**, a high-order, GPU-accelerated solver for compressible flows.

The dataset isolates the coupled role of **momentum**, **buoyancy**, and **temperature ratio** in shaping jet attachment and lift-off, offering a modern benchmark for:
- turbulence-model development (RANS, LES, WMLES),
- validation studies,
- reduced-order modelling,
- canonical comparisons across blowing and temperature ratios.

---

## 📁 Repository Structure

```
film-cooling-database/
├── wall/
│   ├── friction-coefficient/
│   ├── adiabatic-effectiveness/
│   └── ...
├── mean-fields/
│   ├── velocity/
│   ├── temperature/
│   └── ...
├── jets/
│   ├── profiles/
│   └── data/
└── README.md
```

All files are **plain-text tables** (`.txt`) with headers and can be loaded directly in Python, MATLAB, ParaView, Tecplot, etc.

---

## 🧩 Simulation Matrix

| Parameter | Symbol | Values |
|----------|--------|--------|
| Freestream Mach number | $begin:math:text$M\_\\infty$end:math:text$ | 0.8, 1.2, 1.6 |
| Coolant temperature ratio | $begin:math:text$T\_c\/T\_r$end:math:text$ | 0.50, 0.75 |
| Wall condition | — | Adiabatic |
| Geometry | — | Round hole, 30° inclination |
| Grid resolution | — | $begin:math:text$2000 \\times 384 \\times 128$end:math:text$ |
| LES closure | — | WALE |
| Solver | — | URANOS (GPU-accelerated) |

---

## 📐 Key Quantities

| Symbol | Description | Normalization |
|--------|-------------|---------------|
| $begin:math:text$y\^\+$end:math:text$ | wall-normal coordinate | $begin:math:text$y u\_\\tau\/\\nu\_w$end:math:text$ |
| $begin:math:text$u\^\+$end:math:text$ | Van-Driest–transformed velocity | $begin:math:text$\\int\_0\^u \\sqrt\{\\rho\/\\rho\_w\}\\\, du \/ u\_\\tau$end:math:text$ |
| $begin:math:text$T\^\*$end:math:text$ | nondimensional temperature | $begin:math:text$\\tilde\{T\}\/T\_\\infty$end:math:text$ |
| $begin:math:text$\\tau\_\{ij\}\^\+$end:math:text$ | Reynolds stresses | $begin:math:text$\(\\rho\/\\rho\_w\)\\widetilde\{u\_i\'\'u\_j\'\'\}\/u\_\\tau\^2$end:math:text$ |
| $begin:math:text$\\eta$end:math:text$ | adiabatic effectiveness | $begin:math:text$\(T\_r \- T\_w\)\/\(T\_r \- T\_c\)$end:math:text$ |

---

## 📊 Usage Examples

### Python

```python
import numpy as np
import matplotlib.pyplot as plt

# Load a sample wall-friction profile
yplus, cf = np.loadtxt("wall/friction-coefficient/M12_T05_cf.txt", unpack=True)

plt.plot(yplus, cf, "-o", markersize=4)
plt.xlabel(r"$y^+$")
plt.ylabel(r"$c_f$")
plt.grid(True)
plt.show()
```

### MATLAB

```matlab
data = readmatrix("wall/adiabatic-effectiveness/M16_T075_eta.txt");
yplus = data(:,1);
eta   = data(:,2);

plot(yplus, eta, 'r-o', 'MarkerFaceColor','w');
xlabel('$y^+$','Interpreter','latex');
ylabel('$\eta$','Interpreter','latex');
grid on;
```

---

## 🔍 Why This Database?

This resource provides:

- **High-resolution LES** of a **canonical** film-cooling configuration.  
- **Systematic parameter variation** (blowing ratio + temperature ratio).  
- Clean **plain-text data** for maximally easy ingestion.  
- A **baseline benchmark** for:
  - turbulence modelling,
  - WMLES tuning,
  - heat-transfer studies,
  - RANS/LES comparison,
  - reduced-order model calibration.

The goal is to offer a transparent, reusable, engine-relevant dataset for the research community.

---

## 📥 Download

Clone the repo:

```bash
git clone https://github.com/uranos-gpu/film-cooling-database
```

or download the dataset via the GitHub “Download ZIP” button.

---

## 📖 Citation

To be appeared...

---

## 🙏 Acknowledgements

Supported by:
- **CINECA ISCRA HPC Grants**
- **NVIDIA Academic Hardware Grant**
- **Department of Industrial Engineering — University of Padova**

---

## 📄 License

Released under the **MIT License**.  
Free for academic and educational use **with proper citation**.

---

## 🛠 Contributing

Issues, questions, suggestions, and pull requests are welcome — especially contributions related to:
- post-processing scripts,
- visualization tools,
- additional derived fields.
