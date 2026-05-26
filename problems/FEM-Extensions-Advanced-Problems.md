---
tags: [problems, chapter-3, FEM-extensions, parametric, maximum-principle, nonstandard]
---

# FEM Extensions & Advanced Problems

**Chapter 3 — Non-standard formulations, maximum principle, parametric FE, coupled BVPs**

---

## Problem 3-3: Dirichlet BVP with Point-Evaluation RHS

**Code folder:** `PointEvaluationRhs` | **Sections:** §1.2.3.4, §2.2

**Concepts:** [[Sobolev-Spaces]], [[Variational-Crimes]], [[FEM-Code-Validation]]

**Setup:** The right-hand side functional $\ell(v) = v(x_0)$ (point evaluation) is not bounded on $H^1$ in 2D. Analyze what happens to the FEM solution and its convergence.

| What it tests |
|--------------|
| Ill-posed variational problems |
| Riesz representor of unbounded functionals |
| FEM behavior for singular data |

> [!warning] Common mistake
> Point evaluation is a bounded functional on $H^1$ only in 1D (by Sobolev embedding). In 2D, $H^1 \not\hookrightarrow C^0$, so the variational problem is not well-posed in the standard sense.

> [!abstract] Solution gist
> $\ell(v) = v(x_0) = \delta_{x_0}(v)$. In 2D: $\delta_{x_0} \notin (H^1)^*$ → Lax-Milgram doesn't apply. But: the FEM problem is well-posed (point evaluation is fine on $C^0$ functions, and $S_p^0 \subset C^0$). The FEM solution $u_h$ exists but doesn't converge in $H^1$ to a function in $H^1$. The "solution" has a log-singularity at $x_0$: $u \sim -\frac{1}{2\pi}\log|x - x_0|$ (Green's function). Convergence rate degrades: $\|u - u_h\|_{H^1} = O(h^{1/2})$ instead of $O(h)$.

---

## Problem 3-4: Stationary Heat Conduction BVP

**Code folder:** `UnstableBVP` | **Sections:** §2.7.4, §1.6

**Concepts:** [[Boundary-Conditions-Elliptic]], [[FEM-Code-Validation]]

**Setup:** Reverse-engineer a BVP from its variational formulation. Compute FEM solution and measure empirical convergence.

| What it tests |
|--------------|
| Deriving strong PDE from variational form |
| Empirical convergence analysis |
| Identifying convergence rate from data |

> [!abstract] Solution gist
> Given variational form → reverse-engineer PDE by integration by parts. Solve with LehrFEM++, compute errors on refined meshes. If the BVP has a sign-changing reaction coefficient $\gamma(\mathbf{x})$ that makes $a$ not coercive, the problem may be "unstable" — convergence can be erratic. Identify from data: if errors don't decrease monotonically or rates are below expected, suspect loss of coercivity.

---

## Problem 3-7: Maximum Principle for Reaction-Diffusion BVP

**Code folder:** `MaximumPrinciple` | **Sections:** §3.7, §4.1

**Concepts:** [[Variational-Crimes]], [[A-Priori-FEM-Error-Estimates]]

**Sub-tasks:** a–g

**Setup:** Verify whether the continuous and discrete maximum principles hold for a reaction-diffusion BVP. Check under what mesh conditions the discrete principle is satisfied.

| What it tests |
|--------------|
| Continuous maximum principle (Thm 3.7.1.2) |
| Discrete maximum principle (Thm 3.7.2.20) |
| Mesh conditions (acute triangulations, Delaunay property) |

> [!warning] Key insight
> The discrete maximum principle requires all angles in the triangulation to be acute ($\leq \pi/2$). Obtuse triangles can produce non-physical oscillations in the discrete solution.

> [!abstract] Solution gist
> Continuous max principle: $-\Delta u + \gamma u = f \geq 0$, $u|_{\partial\Omega} \geq 0$ → $u \geq 0$ in $\Omega$ (if $\gamma \geq 0$). Discrete analogue (Thm 3.7.2.20): $\mathbf{A}\boldsymbol{\mu} = \boldsymbol{\phi}$ with $\boldsymbol{\phi} \geq 0$ → $\boldsymbol{\mu} \geq 0$ iff $\mathbf{A}$ is an M-matrix. For linear FEM: $\mathbf{A}$ is M-matrix iff all off-diagonals $\leq 0$ iff all triangle angles $\leq \pi/2$ (Delaunay condition for pure Laplacian). With reaction $\gamma > 0$: mass matrix has positive off-diagonals, can destroy M-matrix property. Test: create obtuse triangle mesh, observe oscillations.

---

## Problem 3-10: Parametric Finite Elements

**Code folder:** `ParametricFiniteElements` | **Sections:** §2.8, §2.8.3

**Concepts:** [[Parametric-FEM]], [[Variational-Crimes]]

**Sub-tasks:** a–b

**Setup:** Map a BVP on a complicated domain to a simpler reference domain via a parametric map. Implement element matrix computation for parametric elements.

| What it tests |
|--------------|
| Parametric FEM for domain transformation |
| Non-affine element maps (non-constant Jacobian) |
| Quadrature on parametric elements |
| Variational crimes from geometry approximation |

> [!abstract] Solution gist
> Map complicated domain $\Omega$ to unit square via $\Phi$. Solve on simple domain with transformed BVP: coefficients become $\alpha(\hat{\mathbf{x}}) = \frac{\mathbf{F}_\Phi^{-1}\mathbf{F}_\Phi^{-\top}}{|\det\mathbf{F}_\Phi|}$. Element matrices on physical domain via transformation formula (Lemma 2.8.3.10). Non-affine map → Jacobian varies within element → need quadrature. This is a "variational crime" if the geometry is only approximated (e.g., curved boundary replaced by polygon) → Strang's Lemma bounds the additional error.

---

## Problem 3-16: Non-Conforming Crouzeix-Raviart FEM (Theory)

**Code folder:** `NonConformingCrouzeixRaviartFiniteElements` | **Sections:** §2.8.1

**Concepts:** [[Crouzeix-Raviart-FEM]], [[Lagrangian-FEM]]

**Sub-tasks:** a–c

**Setup:** Analyze the Crouzeix-Raviart element (DOFs at edge midpoints, not globally continuous). Prove convergence despite non-conformity.

| What it tests |
|--------------|
| Non-conforming elements (not in $H^1$) |
| Modified error analysis for non-conforming FEM |
| Comparison with conforming elements |

> [!abstract] Solution gist
> Crouzeix-Raviart: $V_h \not\subset H^1$ (functions discontinuous across edges). Error analysis: can't use standard Céa (requires $V_h \subset V$). Instead: Strang-type analysis — split error into best approximation + consistency. Consistency term: $\sum_e \int_e [\![u_h]\!] \cdot \nabla v\,\mathrm{d}S = 0$ for $v \in H^2$ by the midpoint rule property (edge midpoint values match → jump integral vanishes for linears). Result: same $O(h)$ convergence in broken $H^1$ norm as conforming $p=1$.

---

## Problem 3-20: First-Order System Least-Squares Variational Formulation

**Code folder:** `—`

**Concepts:** [[Linear-Variational-Problem]], [[A-Priori-FEM-Error-Estimates]]

**Sub-tasks:** a–e

**Setup:** Reformulate a second-order elliptic BVP as a first-order system and apply a least-squares variational principle.

| What it tests |
|--------------|
| Alternative variational formulations |
| Least-squares FEM (inherently s.p.d.) |
| Error analysis for FOSLS |

> [!abstract] Solution gist
> Rewrite $-\Delta u = f$ as first-order system: $\boldsymbol{\sigma} = \nabla u$, $-\text{div}\,\boldsymbol{\sigma} = f$. Least-squares functional: $J(\boldsymbol{\tau}, v) = \|\boldsymbol{\tau} - \nabla v\|_{L^2}^2 + \|\text{div}\,\boldsymbol{\tau} + f\|_{L^2}^2$. Minimizer solves the original problem. Advantage: the bilinear form is automatically s.p.d. (it's a sum of squares), so no inf-sup condition needed. Disadvantage: requires $H(\text{div})$-conforming spaces for $\boldsymbol{\sigma}$ or accepts non-conforming approximation.

---

## Problem 3-22: Coupled Elliptic Boundary Value Problems

**Code folder:** `CoupledBVPs` | **Sections:** §1.8, §2.7

**Concepts:** [[Boundary-Conditions-Elliptic]], [[Assembly-Algorithm]]

**Sub-tasks:** a–c

**Setup:** System of unidirectionally coupled elliptic BVPs. Assembly and solution of the coupled system.

| What it tests |
|--------------|
| Systems of elliptic PDEs |
| Coupled variational formulations |
| Block system assembly in LehrFEM++ |

> [!abstract] Solution gist
> Two BVPs coupled one-way: solve first BVP for $u$, then use $u$ as data in second BVP for $w$. Block system: $\begin{pmatrix}\mathbf{A}_u & \mathbf{0}\\\mathbf{C} & \mathbf{A}_w\end{pmatrix}\begin{pmatrix}\boldsymbol{\mu}_u\\\boldsymbol{\mu}_w\end{pmatrix} = \begin{pmatrix}\boldsymbol{\phi}_u\\\boldsymbol{\phi}_w\end{pmatrix}$. Lower-triangular → solve sequentially. In LehrFEM++: assemble each block separately into sub-blocks of a large COOMatrix, or solve two independent systems in sequence using the solution of the first as input to the second.

---

## Problem 3-23: Neumann Data by Projection

**Code folder:** `NeumannDataRecovery` | **Sections:** §2.7

**Concepts:** [[Boundary-Conditions-Elliptic]], [[FEM-Code-Validation]]

**Sub-tasks:** a–d

**Setup:** Recover Neumann data (boundary flux $\nabla u \cdot \mathbf{n}$) from a FEM solution via $L^2$ projection.

| What it tests |
|--------------|
| Flux recovery / post-processing |
| $L^2$ projection onto boundary FE space |
| Superconvergent flux computation |

> [!abstract] Solution gist
> Raw FEM flux $\nabla u_h \cdot \mathbf{n}$ is piecewise constant on boundary edges (one order less accurate than $u_h$). Recovery: $L^2$-project onto continuous piecewise linear boundary FE space. Boundary mass matrix: $\mathbf{M}^\partial_{ij} = \int_{\partial\Omega} b_i^h b_j^h\,\mathrm{d}S$. Boundary load: $\phi_i^\partial = \int_{\partial\Omega} (\nabla u_h \cdot \mathbf{n}) b_i^h\,\mathrm{d}S$ (edge-by-edge integration). Solve $\mathbf{M}^\partial\boldsymbol{\lambda} = \boldsymbol{\phi}^\partial$. Result: smoother flux with potentially superconvergent accuracy.

---

## Problem 3-24: Axisymmetric Boundary Value Problem

**Code folder:** `developers/MaxwellEvlTM` | **Sections:** §1.2.1, §2.7.2

**Concepts:** [[Electromagnetic-Wave-Equations]], [[Variational-Crimes]]

**Sub-tasks:** a–d

**Setup:** 3D BVP with axial symmetry reduced to 2D. Weighted Sobolev spaces in cylindrical coordinates.

| What it tests |
|--------------|
| Dimension reduction via symmetry |
| Weighted bilinear forms in cylindrical coords |
| Full LehrFEM++ pipeline on non-standard BVP |

> [!abstract] Solution gist
> 3D problem with rotational symmetry → reduce to 2D in $(r, z)$ coordinates. The volume element $r\,\mathrm{d}r\,\mathrm{d}z$ introduces a weight $r$ into all integrals. Weighted bilinear form: $a(u,v) = \int r\,\nabla u \cdot \nabla v\,\mathrm{d}r\,\mathrm{d}z$. In LehrFEM++: use `lf::mesh::utils::MeshFunctionGlobal` for the weight $r = x_1$ (first coordinate), pass as coefficient to `ReactionDiffusionElementMatrixProvider`. Weighted mass matrix similarly. Careful: $r = 0$ on the symmetry axis → degenerate weight.

---

**Related concepts:** [[Parametric-FEM]], [[Variational-Crimes]], [[Lagrangian-FEM]], [[Boundary-Conditions-Elliptic]]
