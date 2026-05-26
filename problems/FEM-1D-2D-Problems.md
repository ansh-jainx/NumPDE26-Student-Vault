---
tags: [problems, chapter-2, FEM, Galerkin, 1D, 2D, element-matrices]
---

# FEM 1D/2D Problems

Problems from Chapter 2 covering §2.2–§2.4: Galerkin discretization theory, linear FEM in 1D and 2D, element matrix computation, convergence testing.

---

## Problem 2-1: Properties of Galerkin Solutions

**Sections:** §2.2

**Concepts:** [[Galerkin-Discretization]], [[Galerkin-Orthogonality]], [[Lax-Milgram-Theorem]]

**Setup:** Theoretical properties of Galerkin solutions: Galerkin orthogonality, best approximation, effect of enlarging the FE space.

| What it tests |
|--------------|
| Galerkin orthogonality $a(u - u_h, v_h) = 0$ |
| Best approximation property in energy norm |
| Monotonicity: $V_h \subset V_H \Rightarrow \|u - u_h\|_a \leq \|u - u_H\|_a$ |

> [!abstract] Solution gist
> **(a)** Counterexample for non-s.p.d.: take $a$ non-symmetric on $\mathbb{R}^2$ so LBB fails on a subspace. **(b)** S.p.d. $a$ on $V_{h,0} \subset V_0$ → Lax-Milgram applies directly → unique $u_h$. **(c)** Galerkin orthogonality: subtract $a(u_h, v_h) = \ell(v_h)$ from $a(u, v_h) = \ell(v_h)$ → $a(u - u_h, v_h) = 0$. **(d)** Expand $J(u_h) - J(u) = \frac{1}{2}a(u_h, u_h) - \ell(u_h) - \frac{1}{2}a(u,u) + \ell(u)$; add/subtract cross terms, use Galerkin orthogonality → $= \frac{1}{2}\|u - u_h\|_a^2$.

---

## Problem 2-2: Transformation of Galerkin Matrices

**Code folder:** `TransformationOfGalerkinMatrices` | **Sections:** §2.2, §2.4

**Concepts:** [[Galerkin-Matrix]], [[Galerkin-Discretization]]

**Setup:** How the Galerkin matrix transforms under a change of basis. If $\mathbf{b}' = \mathbf{S}\mathbf{b}$, then $\mathbf{A}' = \mathbf{S}^T\mathbf{A}\mathbf{S}$.

| What it tests |
|--------------|
| Basis transformation for Galerkin matrices |
| Condition number dependence on basis choice |

> [!abstract] Solution gist
> **(a)** For $N=4$: $\mathbf{S}$ is a $4 \times 4$ matrix with $\pm 1$ entries — pairs of basis functions are summed/differenced. $\mathbf{S}^\top\mathbf{S}$ is block-diagonal. **(b)** General $N=2M$: $\mathbf{S}$ has block structure, invertible with explicit inverse. **(c)** Each entry $\tilde{A}_{ij} = \sum$ of 4 entries of $\mathbf{A}$ weighted by $\pm 1$ (from the $\pm$ in the basis transformation). **(d)** Dual view: each $(A)_{k,\ell}$ scatters to 4 entries of $\tilde{\mathbf{A}}$ → key insight for COO-format implementation. **(e)** `transformCOOmatrix`: iterate triplets, for each $(k,\ell,a_{k\ell})$ emit 4 new triplets with mapped indices and $\pm a_{k\ell}$ weights. **(f)** S.p.d. $a$ → Gram-Schmidt orthogonalization in $a$-inner product gives basis with $\mathbf{A} = \mathbf{I}$.

---

## Problem 2-3: Pointwise "Exact" Galerkin Solution

**Sections:** §2.3

**Concepts:** [[Linear-FEM-1D]], [[Galerkin-Discretization]]

**Setup:** Show that the Galerkin solution with piecewise linear FEM is exact at mesh nodes for certain right-hand sides. Uses integration by parts in 1D.

| What it tests |
|--------------|
| Superconvergence at nodes (1D linear FEM) |
| Integration by parts technique |

> [!abstract] Solution gist
> For $-u'' = f$ with piecewise linear FEM in 1D: the Galerkin solution $u_h$ satisfies $u_h(x_i) = u(x_i)$ at all mesh nodes when $f$ is piecewise constant. Proof: test with $v_h = b_i^h$ (hat function at node $x_i$) → $a(u_h, b_i^h) = \int f b_i^h$. Integration by parts on $a(u, b_i^h) = -\int u'' b_i^h = \int f b_i^h$ shows $u$ also satisfies the Galerkin equation → by uniqueness $u_h(x_i) = u(x_i)$. This is a superconvergence result special to 1D.

---

## Problem 2-4: Linear Finite Elements for Two-Point BVPs

**Code folder:** `LinearFE1D` | **Sections:** §2.3

**Concepts:** [[Linear-FEM-1D]], [[Galerkin-Matrix]]

**Setup:** Full 1D linear FEM pipeline: tent function basis, element matrices, assembly, solve, convergence study. Variable coefficients $\alpha(x)$, $\gamma(x)$.

| What it tests |
|--------------|
| 1D element stiffness and mass matrices with variable coefficients |
| Assembly in 1D |
| Convergence rates $O(h^p)$ verification |

> [!tip] Key formulas
> Element stiffness: $(\mathbf{A}_e)_{ij} = \int_{x_{k-1}}^{x_k} \alpha\,b_i'\,b_j'\,dx + \int_{x_{k-1}}^{x_k} \gamma\,b_i\,b_j\,dx$. For constant $\alpha$ on element: $\frac{\alpha}{h}[-1,1;-1,1]$.

> [!abstract] Solution gist
> Full 1D pipeline: (1) tent functions $b_i(x)$ on mesh $x_0 < \cdots < x_N$. (2) Element stiffness $\frac{\alpha_e}{h_e}\begin{pmatrix}1&-1\\-1&1\end{pmatrix}$, element mass $\frac{\gamma_e h_e}{6}\begin{pmatrix}2&1\\1&2\end{pmatrix}$. (3) Assemble: loop over elements, scatter into global matrix. (4) Load: $\phi_i = \int f\,b_i \approx \frac{h}{2}(f_{i-1} + f_i)$ (trapezoidal). (5) Dirichlet BCs: fix rows/columns. (6) Solve $\mathbf{A}\boldsymbol{\mu} = \boldsymbol{\phi}$. (7) Convergence: refine $h \to h/2$, check $O(h^2)$ in $L^2$, $O(h)$ in $H^1$ on log-log plot.

---

## Problem 2-5: Triangular Linear FEM for 2D Reaction-Diffusion BVP

**Code folder:** `SimpleLinearFiniteElements` | **Sections:** §2.4

**Concepts:** [[Triangular-Linear-FEM-2D]], [[Galerkin-Matrix]], [[Assembly-Algorithm]]

**Setup:** Complete 2D linear FEM implementation. Assemble stiffness + mass (reaction term), load vector, solve, plot. The "hello world" of 2D FEM.

| What it tests |
|--------------|
| Barycentric coordinates, gradient computation |
| 2D element matrices $\mathbf{A}_K$, $\mathbf{M}_K$ |
| Full assembly + solve pipeline in 2D |
| Convergence study on refined meshes |

> [!warning] Common mistake
> Don't forget the reaction term $\gamma\int_K u\,v$: it contributes via the element mass matrix, not the stiffness matrix. Total element matrix = stiffness + reaction mass.

> [!abstract] Solution gist
> 2D "hello world": (1) Triangle $K$ with vertices $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$. Gradients $\nabla\lambda_i = \frac{1}{2|K|}(\mathbf{a}_j - \mathbf{a}_k)^\perp$ (rotated edge vector). (2) Element stiffness: $(\mathbf{A}_K)_{ij} = |K|\,\nabla\lambda_i \cdot \nabla\lambda_j$. Element mass: $(\mathbf{M}_K)_{ij} = \frac{|K|}{12}(1 + \delta_{ij})$. (3) Load: $\phi_i^K = \frac{|K|}{3}f(\text{barycenter})$ (midpoint rule). (4) Assembly into `COOMatrix`, apply BCs via `FixFlaggedSolutionComponents(selector, A_COO, phi)`, then convert to sparse with `A_COO.makeSparse()`. (5) `ReactionDiffusionElementMatrixProvider(fe_space, mf_alpha, mf_gamma)` handles both stiffness and reaction.

---

## Problem 2-10: Projection onto Gradients

**Code folder:** `ProjectionOntoGradients` | **Sections:** §2.4

**Concepts:** [[Triangular-Linear-FEM-2D]], [[Galerkin-Discretization]]

**Setup:** Compute the $L^2$-projection of a vector field onto the gradient space of the FE space. Requires assembling a non-standard bilinear form.

| What it tests |
|--------------|
| Custom bilinear forms beyond standard stiffness/mass |
| $L^2$-projection technique |

> [!abstract] Solution gist
> Find $u_h \in V_h$ such that $\int_\Omega \nabla u_h \cdot \mathbf{w} = \int_\Omega \mathbf{f} \cdot \mathbf{w}$ for all $\mathbf{w} = \nabla v_h$. This is NOT the Poisson problem — it's an $L^2$-projection of $\mathbf{f}$ onto the gradient space. Galerkin system: $\mathbf{A}\boldsymbol{\mu} = \boldsymbol{\phi}$ where $\mathbf{A}_{ij} = \int \nabla b_i \cdot \nabla b_j$ (standard stiffness) and $\phi_i = \int \mathbf{f} \cdot \nabla b_i$ (non-standard load — involves dot product of $\mathbf{f}$ with basis gradients). Custom `ElementVectorProvider` needed for the RHS.

---

## Problem 2-11: Hybrid-Mesh Galerkin Matrices and RHS Vectors

**Sections:** §2.4

**Concepts:** [[Galerkin-Matrix]], [[Triangular-Linear-FEM-2D]]

**Setup:** Assemble Galerkin matrices on meshes containing both triangles and quadrilaterals. Element matrices differ by cell type.

| What it tests |
|--------------|
| FEM on hybrid meshes (triangles + quads) |
| Different element matrices for different cell types |

> [!abstract] Solution gist
> Key: `cell.RefEl()` distinguishes `kTria` vs `kQuad`. Triangle: 3 local DOFs, $3\times 3$ element matrix. Quad: 4 local DOFs (bilinear shape functions), $4\times 4$ element matrix. For quads, stiffness uses $2\times 2$ Gauss quadrature since the Jacobian is non-constant. `AssembleMatrixLocally` handles both cell types seamlessly — the provider's `Eval` dispatches on `RefEl`.

---

## Problem 2-16: Rigidity of Piecewise Polynomial Continuous Functions

**Code folder:** `—` | **Sections:** §2.5

**Concepts:** [[Lagrangian-FEM]]

**Setup:** Investigate when a piecewise polynomial FE space degenerates (becomes "too rigid") on special mesh configurations.

| What it tests |
|--------------|
| FE space dimension vs mesh topology |
| Degenerate cases in non-standard meshes |

> [!abstract] Solution gist
> On special meshes (e.g., a single quad split into 4 triangles sharing a vertex), continuous piecewise polynomials of degree $p$ may have fewer DOFs than expected. The global continuity constraints over-determine the space. Investigation: count local DOFs, subtract continuity constraints across edges, compare with expected dimension. When the space "degenerates," certain configurations of function values become impossible.

---

## Problem 2-19: Lagrangian FE on Criss-Cross Meshes

**Code folder:** `—` | **Sections:** §2.5, §2.6

**Concepts:** [[Lagrangian-FEM]]

> [!warning] Exam alert
> **2023 Midterm 0-2** (`FESpacesCrissCross`). Deep dive: [[Exam-Deep-Element-Matrices#Criss-cross]].

**Setup:** Lagrangian FEM on criss-cross (diagonal) mesh patterns. Special properties of the resulting FE spaces.

| What it tests |
|--------------|
| FE spaces on structured meshes |
| Macro-element techniques |

> [!abstract] Solution gist
> Criss-cross mesh: unit square divided by horizontal, vertical, and diagonal lines. The resulting FE space $S_p^0(\mathcal{M})$ has special properties — e.g., for $p=1$ on criss-cross, piecewise linear functions can represent more than just global linears. Macro-element analysis: on the $2\times 2$ macro-element, count constraints to find the actual dimension. Useful for understanding how mesh topology affects approximation power.

---

## Problem 2-23: Galerkin Matrices

**Code folder:** `TransformationOfGalerkinMatrices` | **Sections:** §2.2, §2.4

**Concepts:** [[Galerkin-Matrix]], [[Galerkin-Discretization]]

**Setup:** Compute and analyze properties of Galerkin matrices for specific BVPs. Sparsity pattern, symmetry, positive definiteness.

| What it tests |
|--------------|
| Galerkin matrix properties |
| Sparsity and conditioning |

> [!abstract] Solution gist
> Analyze Galerkin matrices for specific small meshes: compute element matrices by hand, assemble, verify symmetry and positive definiteness. Sparsity pattern: $A_{ij} \neq 0$ only if basis functions $b_i, b_j$ have overlapping support (share a cell). Bandwidth depends on node numbering. Condition number $\kappa(\mathbf{A}) = O(h^{-2})$ for the stiffness matrix of linear FEM.

---

**Exams:** Midterm 0-2 appears in multiple years with varying focus (see week-specific exam tables); element matrix computation is a recurring pattern.

---

**Related concepts:** [[Galerkin-Discretization]], [[Linear-FEM-1D]], [[Triangular-Linear-FEM-2D]], [[Galerkin-Matrix]], [[Galerkin-Orthogonality]], [[Formulas-FEM-Assembly]]
