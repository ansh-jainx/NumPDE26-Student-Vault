---
tags: [problems, chapter-3, error-analysis, convergence, duality, output-functionals]
---

# FEM Error Analysis Problems

**Chapter 3 — A priori estimates, convergence rates, interpolation, output functionals, duality**

---

## Problem 3-1: Computing Averages over the Boundary

**Sections:** §3.6

**Concepts:** [[A-Priori-FEM-Error-Estimates]], [[Cea-Lemma]], [[FEM-Code-Validation]]

**Setup:** Compute a boundary average $\int_{\partial\Omega} u\,\mathrm{d}S$ as a linear output functional. Analyze convergence of the FEM approximation using duality.

| What it tests |
|--------------|
| Linear output functional formulation |
| Duality argument for enhanced convergence |
| Boundary integral computation in LehrFEM++ |

> [!abstract] Solution gist
> Output functional $J(u) = \int_{\partial\Omega} u\,\mathrm{d}S = \ell(u)$ where $\ell(v) = \int_{\partial\Omega} v\,\mathrm{d}S$. By Aubin-Nitsche duality (Thm 3.6.1.7): $|J(u) - J(u_h)| \leq C h^{2p}$ for smooth solutions on convex domains (double the $H^1$ rate). Compute via boundary edge loop: `for (edge on ∂Ω) sum += lf::geometry::Volume(*edge->Geometry()) * (mu[i] + mu[j]) / 2`.

---

## Problem 3-2: Debugging Finite Element Codes

**Code folder:** `DebuggingFEM` | **Sections:** §3.3.5, §3.8, §2.7

**Concepts:** [[FEM-Code-Validation]], [[A-Priori-FEM-Error-Estimates]]

**Setup:** Given a LehrFEM++ FEM implementation with bugs. Use convergence rate analysis to identify and fix errors.

| What it tests |
|--------------|
| Code validation via convergence rates (§3.8) |
| Empirical convergence analysis on log-log plots |
| Identifying assembly or BC bugs from rate degradation |

> [!tip] Exam-relevant skill
> The §3.8 validation recipe appears in multiple exam problems: solve on refined meshes, check log-log slopes match predicted rates.

> [!abstract] Solution gist
> Validation recipe from §3.8: pick known exact solution $u^*$, manufacture $f = -\Delta u^*$, solve FEM on sequence of refined meshes, compute $\|u^* - u_h\|_{H^1}$ and $\|u^* - u_h\|_{L^2}$, plot on log-log. Expected slopes: $p$ ($H^1$), $p+1$ ($L^2$). If slopes are wrong → bug. Common bugs: wrong Jacobian in element matrix (affects all rates), BC not applied (reduces $H^1$ rate to 0), load vector wrong sign (solution is wrong but rates may look OK).

---

## Problem 3-5: Error Estimates for Traces

**Code folder:** `ErrorEstimatesForTraces` | **Sections:** §3.3

**Concepts:** [[Interpolation-Error-Estimates]], [[A-Priori-FEM-Error-Estimates]]

**Sub-tasks:** a–i

**Setup:** Derive a priori error estimates for the trace $u|_{\partial\Omega}$ of FEM solutions. Prove and verify convergence of boundary values.

| What it tests |
|--------------|
| Interpolation error for traces (boundary values) |
| Combining Céa's Lemma with trace inequalities |
| Convergence rate verification in LehrFEM++ |

> [!abstract] Solution gist
> Trace error: $\|u - u_h\|_{L^2(\partial\Omega)} \leq C\|u - u_h\|_{H^1(\Omega)}^{1/2}\|u - u_h\|_{L^2(\Omega)}^{1/2}$ (multiplicative trace inequality). With Céa + interpolation: $O(h^p) \cdot O(h^{p+1})^{1/2} = O(h^{p+1/2})$. Alternatively, direct interpolation estimate on boundary edges. LehrFEM++: compute boundary $L^2$ error via edge quadrature, comparing `lf::fe::MeshFunctionFE` with the exact boundary trace.

---

## Problem 3-6: Projection Onto Constants

**Code folder:** `—` | **Sections:** §3.3.1

**Concepts:** [[Interpolation-Error-Estimates]]

**Setup:** Analyze $L^2$ and $H^1$ interpolation error for projection onto piecewise constants.

| What it tests |
|--------------|
| $L^2$ projection error estimates |
| Interpolation theory in simplest setting |
| Comparison with piecewise linear interpolation |

> [!abstract] Solution gist
> Projection onto piecewise constants ($p=0$): $\Pi_0 u|_K = \frac{1}{|K|}\int_K u$. Interpolation error: $\|u - \Pi_0 u\|_{L^2(K)} \leq h_K |u|_{H^1(K)}$ (Bramble-Hilbert). Global: $\|u - \Pi_0 u\|_{L^2} = O(h)$. No $H^1$ convergence since $\Pi_0 u$ is discontinuous. Compare: piecewise linear gives $O(h^2)$ in $L^2$, $O(h)$ in $H^1$.

---

## Problem 3-8: Output Functionals with Impedance BCs

**Code folder:** `OutputImpedanceBVP` | **Sections:** §1.8, §3.6

**Concepts:** [[Boundary-Conditions-Elliptic]], [[A-Priori-FEM-Error-Estimates]]

**Setup:** Compute output functionals for an elliptic BVP with impedance (Robin) boundary conditions. Analyze convergence via duality.

| What it tests |
|--------------|
| Robin/impedance BC variational formulation |
| Output functional convergence (Aubin-Nitsche duality) |
| Enhanced convergence rates for smooth solutions |

> [!abstract] Solution gist
> Robin/impedance BC: $\nabla u \cdot \mathbf{n} + \alpha u = g$ on $\partial\Omega$. Variational form: $a(u,v) = \int_\Omega \nabla u \cdot \nabla v + \alpha\int_{\partial\Omega} uv\,\mathrm{d}S$, $\ell(v) = \int_\Omega fv + \int_{\partial\Omega} gv\,\mathrm{d}S$. Output functional $J(u_h)$: apply Aubin-Nitsche → enhanced convergence $O(h^{2p})$ if dual problem has full regularity. Assembly: stiffness + `MassEdgeMatrixProvider(fe_space, mf_alpha, bd_selector)` via `AssembleMatrixLocally(1, ...)` for the Robin boundary term.

---

## Problem 3-11: Stable Evaluation at a Point

**Code folder:** `StableEvaluationAtAPoint` | **Sections:** §3.6.2

**Concepts:** [[Interpolation-Error-Estimates]], [[Sobolev-Spaces]]

**Sub-tasks:** a–c

**Setup:** Point evaluation $u(x_0)$ is an unbounded functional on $H^1$. Convert it into a bounded output functional via regularization.

| What it tests |
|--------------|
| Unbounded vs bounded functionals |
| Regularization of point evaluation |
| Duality for output convergence |

> [!abstract] Solution gist
> Point evaluation $u(x_0)$ is unbounded on $H^1(\Omega)$ for $\Omega \subset \mathbb{R}^2$. Regularize: replace $\delta_{x_0}$ with a mollified version $\ell_\epsilon(v) = \frac{1}{|B_\epsilon|}\int_{B_\epsilon(x_0)} v$ (average over small ball). This is bounded on $H^1$. FEM approximation: $|u(x_0) - \ell_\epsilon(u_h)|$ has two sources of error — mollification $O(\epsilon)$ and FEM $O(h^{2p})$ for the regularized functional. Balance $\epsilon \sim h^{2p}$. In practice: evaluate $u_h(x_0)$ directly (well-defined for FEM since $u_h \in C^0$).

---

## Problem 3-12: Computation of Electrostatic Forces

**Code folder:** `ElectrostaticForce` | **Sections:** §3.6.1, §3.6.3

**Concepts:** [[FEM-Code-Validation]], [[A-Priori-FEM-Error-Estimates]]

**Sub-tasks:** a–d

**Setup:** Compute electrostatic forces as output functionals of an elliptic BVP. Use duality for enhanced convergence.

| What it tests |
|--------------|
| Continuous linear output functional (§3.6.1) |
| Aubin-Nitsche duality (Thm 3.6.1.7) |
| Enhanced convergence via duality |

> [!abstract] Solution gist
> Force = output functional of the field solution: $F = J(u) = \int_\Gamma g(\nabla u)\,\mathrm{d}S$ or similar. Linear output functional → apply Thm 3.6.1.7 (Aubin-Nitsche): $|J(u) - J(u_h)| \leq C\|u - u_h\|_{H^1}\|z - z_h\|_{H^1}$ where $z$ solves the dual problem $a(v, z) = J(v)$. If dual solution $z \in H^2$ → enhanced rate $O(h^{2p})$. LehrFEM++: compute $J(u_h)$ as boundary integral via edge quadrature.

---

## Problem 3-13: Computation of Stationary Currents

**Code folder:** `StationaryCurrents` | **Sections:** §1.8, §3.6.2

**Concepts:** [[Boundary-Conditions-Elliptic]], [[FEM-Code-Validation]]

**Sub-tasks:** a–b

**Setup:** Electromagnetic scalar elliptic BVP. Compute current as boundary flux.

| What it tests |
|--------------|
| Boundary flux as output functional |
| Duality for flux convergence |
| Elliptic BVP with mixed boundary conditions |

> [!abstract] Solution gist
> Current = boundary flux $I = \int_{\Gamma} \nabla u \cdot \mathbf{n}\,\mathrm{d}S$. This is NOT a bounded functional of $u$ (involves derivatives on boundary). Rewrite via Green's formula: $I = \ell(v_0) - a(u, v_0)$ for suitable $v_0$ → becomes bounded output functional. Then duality gives enhanced convergence. Mixed BCs: Dirichlet on $\Gamma_D$, Neumann on $\Gamma_N$ → split boundary terms in variational form.

---

## Problem 3-14: A Local Quasi-Interpolation Operator

**Code folder:** `QuasiInterpolation` | **Sections:** §2.6, §2.4.3

**Concepts:** [[Interpolation-Error-Estimates]], [[Lagrangian-FEM]]

**Sub-tasks:** a–c

**Setup:** Construct a quasi-interpolation operator with local support and prove approximation properties.

| What it tests |
|--------------|
| Quasi-interpolation (alternative to nodal interpolation) |
| Locality and stability of interpolation operators |
| Approximation properties without pointwise evaluation |

> [!abstract] Solution gist
> Quasi-interpolation $Q_h u$: instead of nodal values $u(x_i)$ (which need pointwise evaluation, problematic for $u \in H^1$ in 2D), use local averages: $(Q_h u)(x_i) = \frac{1}{|\omega_i|}\int_{\omega_i} u$ where $\omega_i$ is the support patch of $b_i^h$. Properties: (1) locality — $Q_h u|_K$ depends only on $u$ in neighboring cells, (2) polynomial reproduction — $Q_h p = p$ for $p \in \mathcal{P}_1$, (3) stability — $\|Q_h u\|_{H^1} \leq C\|u\|_{H^1}$. Approximation: same rates as nodal interpolation but defined for rougher $u$.

---

## Problem 3-15: Asymptotic Convergence of FE Discretization & Interpolation Errors

**Sections:** §3.3.2 *(theoretical — no code)*

**Concepts:** [[A-Priori-FEM-Error-Estimates]], [[Cea-Lemma]]

> [!warning] Exam alert
> **2021 Midterm 0-2**; related endterm/finals plots. Deep dive: [[Exam-Deep-Convergence-Plots]].

**Sub-tasks:** a–b

**Setup:** Qualitatively and quantitatively predict asymptotic convergence behavior of FEM errors and interpolation errors based on Thm 3.3.2.21.

| What it tests |
|--------------|
| Applying Thm 3.3.2.21 to predict convergence rates |
| Distinguishing FEM error from interpolation error |
| Understanding role of solution regularity |

> [!abstract] Solution gist
> Apply Thm 3.3.2.21 / Thm 3.3.5.6: $\|u - I_p u\|_{H^l} \leq Ch^{\min(p+1,k)-l}|u|_{H^k}$. For given $u$ regularity ($u \in H^k$) and FE degree $p$: rate in $H^1$ ($l=1$) is $\min(p, k-1)$; rate in $L^2$ ($l=0$) is $\min(p+1, k)$. FEM error ≤ interpolation error (by Céa). Example: $p=2$, $u \in H^3$ → $O(h^2)$ in $H^1$, $O(h^3)$ in $L^2$. If $u \in H^2$ only (corner singularity) → $O(h)$ in $H^1$ regardless of $p$.

---

## Problem 3-19: Convergence of Finite-Element Solutions

**Sections:** §3.2.3 *(theoretical — no code)*

**Concepts:** [[Algebraic-vs-Exponential-Convergence]]

> [!warning] Exam alert
> **2023 Endterm 0-1** (identifying rates from plots). Deep dive: [[Exam-Deep-Convergence-Plots#2023 Endterm 0-1]].

**Sub-tasks:** a

**Setup:** Identify convergence types (algebraic/exponential) from given error data.

| What it tests |
|--------------|
| Identifying algebraic vs exponential convergence (Def 3.2.2.1) |
| Reading convergence rates from numerical data |

> [!abstract] Solution gist
> Given error data at mesh levels: compute successive ratios $e_{k}/e_{k+1}$. Algebraic $O(h^p)$: ratio $\approx 2^p$ under uniform refinement (straight line on log-log plot, slope = $p$). Exponential $O(e^{-\beta N^\gamma})$: ratio grows — curve bends downward on log-log. Distinguish by checking if log-log slope is constant (algebraic) or increasing (exponential).

---

## Problem 3-21: Asymptotic Convergence of FE Solutions

**Code folder:** `AsymptoticCvgFEM` | **Sections:** §3.3.5

**Concepts:** [[FEM-Code-Validation]], [[A-Priori-FEM-Error-Estimates]]

**Sub-tasks:** a

**Setup:** Verify algebraic convergence rates of FEM solutions through numerical experiments.

| What it tests |
|--------------|
| Empirical convergence rate verification |
| Comparison with theoretical predictions from Thm 3.3.5.6 |
| Log-log convergence plots |

> [!abstract] Solution gist
> Concrete verification of Thm 3.3.5.6: solve on mesh levels $L=0,1,2,\ldots$, compute $\|u - u_h\|_{H^1}$ and $\|u - u_h\|_{L^2}$ using `lf::fe::MeshFunctionFE`, `lf::fe::MeshFunctionGradFE`, and `lf::fe::IntegrateMeshFunction`. Plot $h$ vs error on log-log. Measure slope = convergence rate. For $p=1$, smooth $u$: expect slope 1 ($H^1$), slope 2 ($L^2$). For $p=2$: slope 2 ($H^1$), slope 3 ($L^2$).

---

**Related concepts:** [[Cea-Lemma]], [[Interpolation-Error-Estimates]], [[A-Priori-FEM-Error-Estimates]], [[Elliptic-Regularity]], [[FEM-Code-Validation]], [[Algebraic-vs-Exponential-Convergence]]
