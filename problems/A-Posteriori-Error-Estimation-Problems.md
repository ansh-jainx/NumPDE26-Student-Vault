---
tags: [problems, chapter-3, a-posteriori, error-estimation, adaptive]
---

# A Posteriori Error Estimation Problems

**Chapter 3 — Zienkiewicz-Zhu, residual-based, and hierarchical error estimators**

> [!info] A posteriori vs a priori
> A priori estimates predict convergence rates from solution regularity (before solving). A posteriori estimators compute **local error indicators from the computed solution** (after solving), enabling adaptive mesh refinement.

---

## Problem 3-9: Zienkiewicz-Zhu A-Posteriori Error Estimator

**Code folder:** `ZienkiewiczZhuEstimator`

**Concepts:** [[FEM-Code-Validation]], [[A-Priori-FEM-Error-Estimates]]

**Sub-tasks:** a–e

**Setup:** Implement the Zienkiewicz-Zhu (ZZ) error estimator, which computes a recovered gradient $G_h(\nabla u_h)$ by local averaging and uses the difference $\|G_h(\nabla u_h) - \nabla u_h\|$ as error indicator.

| What it tests |
|--------------|
| Gradient recovery by local averaging |
| Element-wise error indicators |
| Effectivity index (ratio of estimator to true error) |
| Driving adaptive mesh refinement |

> [!tip] Key idea
> The ZZ estimator is based on the observation that a post-processed gradient (by local $L^2$ projection onto continuous FE space) is often more accurate than the raw FEM gradient $\nabla u_h$.

> [!abstract] Solution gist
> ZZ gradient recovery: $\nabla u_h$ is piecewise constant (for $p=1$). Project onto continuous piecewise linear space: $G_h(\nabla u_h)(x_i) = \frac{1}{|\omega_i|}\sum_{K \ni x_i} |K|\,\nabla u_h|_K$ (area-weighted average at each node). Error indicator per cell: $\eta_K^2 = \|G_h(\nabla u_h) - \nabla u_h\|_{L^2(K)}^2$. Global estimator: $\eta = (\sum_K \eta_K^2)^{1/2}$. Effectivity index $\eta/\|u - u_h\|_{H^1}$ should be close to 1 for smooth solutions. Implement: compute $G_h$ nodal values by patch averaging, then integrate difference per cell.

---

## Problem 3-17: Residual-Based A-Posteriori Error Estimator

**Code folder:** `ResidualErrorEstimator`

**Concepts:** [[FEM-Code-Validation]], [[A-Priori-FEM-Error-Estimates]]

**Sub-tasks:** a–c

**Setup:** Implement the residual error estimator: the element residual $R_K = f + \Delta u_h|_K$ and edge jumps $J_e = [\![\nabla u_h]\!]_e \cdot \mathbf{n}_e$ bound the error from above and below.

| What it tests |
|--------------|
| Element residuals and edge jump terms |
| Upper bound (reliability) and lower bound (efficiency) |
| Residual-based error indicators per cell |

> [!abstract] Solution gist
> Two components: element residual $R_K = f + \Delta u_h|_K$ (zero for $p=1$ if $f$ is piecewise constant, since $\Delta u_h = 0$ on each cell) and edge jumps $J_e = [\![\nabla u_h]\!]_e \cdot \mathbf{n}_e$ (jump of normal derivatives across internal edges). Indicator: $\eta_K^2 = h_K^2\|R_K\|_{L^2(K)}^2 + \frac{1}{2}\sum_{e \subset \partial K} h_e\|J_e\|_{L^2(e)}^2$. Reliability: $\|u - u_h\|_{H^1}^2 \leq C_\text{rel}\sum_K \eta_K^2$. Efficiency: $\eta_K^2 \leq C_\text{eff}\|u - u_h\|_{H^1(\omega_K)}^2$. In LehrFEM++: loop edges, compute jump of gradients from adjacent cells.

---

## Problem 3-18: Hierarchical Local A-Posteriori Error Estimator

**Code folder:** `HierarchicalErrorEstimator`

**Concepts:** [[FEM-Code-Validation]], [[A-Priori-FEM-Error-Estimates]]

**Sub-tasks:** a–d

**Setup:** Estimate the error by solving local problems on enriched spaces (e.g., adding bubble functions). The local correction magnitudes serve as error indicators.

| What it tests |
|--------------|
| Hierarchical basis enrichment |
| Local error estimation per cell |
| Comparison with residual-based estimator |

> [!abstract] Solution gist
> Enrich local space by adding bubble functions $b_K$ (zero on $\partial K$, positive inside). Solve local problem: find $e_K \in \text{span}(b_K)$ such that $a_K(e_K, b_K) = \ell(b_K) - a_K(u_h, b_K)$ (local residual equation). Indicator: $\eta_K = |e_K|_{H^1(K)}$. Advantages over residual-based: no jump terms, no unknown constants. Disadvantages: requires solving small local problems. The hierarchical basis idea: the error is approximated in the complement space $V_{h/2} \setminus V_h$.

---

**Related concepts:** [[A-Priori-FEM-Error-Estimates]], [[FEM-Code-Validation]], [[Assembly-Algorithm]]
