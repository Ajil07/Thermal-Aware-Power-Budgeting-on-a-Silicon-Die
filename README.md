# Thermal-Aware Power Budgeting on a Silicon Die

### A Unified 6-Stage Mathematical Pipeline from Field Conduction to Linear Programming

**Course:** Capstone Project — PDEs, Transforms & Optimization Techniques (AY 2025–2026)[cite: 12]  
**Department:** Electronics & Communication Engineering & Department of Mathematics  
**Institution:** Saintgits College of Engineering (Autonomous), Kottayam, Kerala  
**Team:** Group 1 (Problem A)[cite: 12, 20]  

---

## 1. Project Overview

In high-performance multi-core processors, asymmetric thread execution leads to localized thermal concentration (hotspots), accelerating transistor aging and inducing thermal throttling[cite: 21, 37]. This project presents an integrated, closed-loop computational continuum linking field physics directly to convex mathematical optimization[cite: 22].

Rather than relying on manual simulation tuning[cite: 22], we derive an automated six-stage mathematical pipeline:
1. **Field Model (Stage 1):** Vector calculus derivation via Fourier's law and energy balance ($\mathbf{q} = -k\nabla T$, $\nabla \cdot \mathbf{q} = Q$)[cite: 14, 23].
2. **PDE Formulation (Stage 2):** Elliptic boundary-value problem on a 2D domain ($\nabla^2 T = -Q/k$) with isothermal Dirichlet boundary conditions ($T_{\mathrm{amb}} = 300\text{ K}$)[cite: 14, 23].
3. **Transform Analysis (Stage 3):** Time-domain Laplace transform yielding dynamic thermal impedance $Z_{\mathrm{th}}(s)$, showing its zero-frequency limit converges to the steady-state thermal resistance matrix $R_{\mathrm{th}}$[cite: 14, 23].
4. **Discretization (Stage 4):** 5-point central difference scheme on a $40 \times 40$ mesh ($1444$ interior nodes), assembled into a sparse Compressed Sparse Row (CSR) matrix system ($A_{\mathrm{int}}\boldsymbol{\theta} = -\frac{1}{k}B\mathbf{p}$).
5. **Epigraph LP Optimization (Stage 5):** Min-max peak temperature converted to a linear program and solved via the HiGHS dual-simplex solver.
6. **Python Verification (Stage 6):** Automated invariant checks and visualization showing a $24.8\text{ K}$ hotspot drop under a strictly conserved $5.0\text{ W}$ budget[cite: 25, 26].

---

## 2. Experimental Benchmark & Key Results

- **Die Dimensions:** $10\text{ mm} \times 10\text{ mm}$, thickness $0.5\text{ mm}$, silicon conductivity $k = 150\text{ W/(m}\cdot\text{K)}$.
- **Mesh Resolution:** $40 \times 40$ grid ($h \approx 0.256\text{ mm}$)[cite: 25].
- **Boundary Conditions:** Dirichlet isothermal $T = 300.0\text{ K}$ on all four edges[cite: 21, 25].
- **Core Coordinates:** 4 symmetric cores located at $(10, 10)$, $(10, 29)$, $(29, 10)$, and $(29, 29)$[cite: 25].
- **Power Constraint:** Total allowable budget $\sum p_i \le 5.0\text{ W}$, with non-negativity $p_i \ge 0$.

| Metric | Unmanaged Baseline | LP-Optimized Result | Milestone Target |
| :--- | :---: | :---: | :---: |
| **Core 1 Allocation ($p_1$)** | $3.20\text{ W}$ (Contention) | $1.25\text{ W}$ | — |
| **Cores 2–4 Allocation ($p_{2,3,4}$)** | $0.60\text{ W}$ each[cite: 26] | $1.25\text{ W}$ each[cite: 26] | — |
| **Total Power Conserved** | $5.00\text{ W}$[cite: 26] | $5.00\text{ W}$[cite: 26] | $\le 5.0\text{ W}$[cite: 17, 24] |
| **Peak Temperature** | **$343.2\text{ K}$**[cite: 26] | **$318.4\text{ K}$**[cite: 26] | — |
| **Temperature Reduction ($\Delta T$)** | — | **$24.8\text{ K}$**[cite: 26] | $\ge 5.0\text{ K}$ |
| **HiGHS Solver Status** | — | **Optimal (Code 7)**[cite: 26] | Feasible / Optimal[cite: 17] |
| **Total Runtime** | — | **$< 2.0\text{ s}$**[cite: 25, 26] | $< 120\text{ s}$[cite: 17] |

---
