---
tags: [week-3, chapter-2, FEM, Galerkin, 1D, 2D, barycentric, exam-critical]
---

# Week 3 — Finite Element Methods I

**Sections:** §2.2–§2.4 | **Chapter 2: Finite Element Methods (FEM)**

---

## Overview

This week turns the continuous variational problem from Ch1 into a computable finite-dimensional system. [[Galerkin-Discretization]] replaces $V$ by $V_h \subset V$ — same variational problem, now a [[Galerkin-Matrix|linear system]]. For 1D, [[Linear-FEM-1D|piecewise linear tent functions]] ([[Linear-FEM-1D]]) yield a tridiagonal system. For 2D, [[Triangular-Linear-FEM-2D|triangular linear FEM]] ([[Triangular-Linear-FEM-2D]]) uses barycentric coordinates. Element matrices: [[Formulas-FEM-Assembly]].

```mermaid
graph LR
    A["Variational Problem on V"] -->|"V_h ⊂ V"| B["Galerkin Problem on V_h"]
    B -->|"basis expansion"| C["Linear System Aμ = φ"]
    C -->|"sparse solver"| D["Solution μ"]
    D -->|"reconstruct"| E["u_h = Σ μ_i b_i"]
    style B fill:#f96
```

---

## Theory Gist

### §2.2 — Galerkin Discretization

Replace $V_0$ by $V_{h,0} \subset V_0$ (finite-dimensional):

$$\text{Find } u_h \in V_h: \quad a(u_h, v_h) = \ell(v_h) \quad \forall v_h \in V_{h,0}$$

> [!theorem] Thm 2.2.1.5 — Existence & uniqueness
> Since $V_{h,0} \subset V_0$ is a Hilbert space, [[Lax-Milgram-Theorem]] applies → unique Galerkin solution exists.

**[[Galerkin-Orthogonality]]:** $a(u - u_h, v_h) = 0$ for all $v_h \in V_{h,0}$ (also in Ch. 3 §3.1.3). This means $u_h$ is the **best approximation** to $u$ from $V_h$ in the energy norm.

**Linear system:** choose basis $\{b_1^h, \ldots, b_N^h\}$, expand $u_h = \sum_j \mu_j b_j^h$:

$$\underbrace{(a(b_j, b_i))_{ij}}_{\mathbf{A}}\,\boldsymbol{\mu} = \underbrace{(\ell(b_i))_i}_{\boldsymbol{\varphi}}$$

([[Galerkin-Matrix]] entries $(\mathbf{A})_{ij} = a(b_j, b_i)$, $(\boldsymbol{\varphi})_i = \ell(b_i)$.)

### §2.3 — [[Linear-FEM-1D|Linear FEM in 1D]]

Mesh $x_0 < x_1 < \cdots < x_{N+1}$ on $[a,b]$. Basis: tent (hat) functions $b_i^h$ — piecewise linear, $b_i^h(x_j) = \delta_{ij}$.

For uniform mesh (step $h$):

> [!info] 1D Element Matrices
> **Element stiffness** (one interval): $\frac{1}{h}\begin{pmatrix}1 & -1 \\ -1 & 1\end{pmatrix}$
>
> **Element mass:** $\frac{h}{6}\begin{pmatrix}2 & 1 \\ 1 & 2\end{pmatrix}$
>
> **Global stiffness:** $\frac{1}{h}\,\mathrm{tridiag}(-1,2,-1)$, **global mass:** $\frac{h}{6}\,\mathrm{tridiag}(1,4,1)$

### §2.4 — [[Triangular-Linear-FEM-2D|Triangular Linear FEM in 2D]]

Triangle $K$ with vertices $\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3$. Local basis = barycentric coordinates $\lambda_1, \lambda_2, \lambda_3$.

> [!info] 2D Element Matrices
> **Element stiffness (Eq. 2.4.5.12):** $(\mathbf{A}_K)_{ij} = |K|\,\nabla\lambda_i \cdot \nabla\lambda_j$
> $$\mathbf{A}_K = |K|\,\mathbf{G}_K^T\,\mathbf{G}_K$$
> where $\mathbf{G}_K \in \mathbb{R}^{2\times 3}$ has columns $\nabla\lambda_i$ (matching `gradbarycoordinates`, Code 2.4.5.11).
>
> **Element mass:** $(\mathbf{M}_K)_{ij} = \frac{|K|}{12}(1 + \delta_{ij})$
> $$\mathbf{M}_K = \frac{|K|}{12}(\mathbf{I} + \mathbf{1}\mathbf{1}^T)$$

> [!warning] Computing gradients of barycentric coordinates
> $\nabla\lambda_i$ are constant on each triangle. `gradbarycoordinates` (Code 2.4.5.11) solves the $3\times 3$ system from Eq. 2.4.5.10 and returns the $2\times 3$ gradient matrix $\mathbf{G}_K$.

---

## Method Recipes

### Recipe 1: Set up the Galerkin system for a 1D BVP

1. Discretize $[a,b]$ with $N$ interior nodes, uniform step $h$
2. Basis: tent functions $b_1^h, \ldots, b_N^h$
3. Stiffness matrix: $\mathbf{A} = \frac{1}{h}\,\mathrm{tridiag}(-1,2,-1)$ (for $-u'' = f$)
4. Load vector: $\varphi_i = \int_a^b f\,b_i^h\,dx \approx h\,f(x_i)$ (midpoint rule)
5. Solve $\mathbf{A}\boldsymbol{\mu} = \boldsymbol{\varphi}$

### Recipe 2: Compute element matrices for a given triangle

Given vertices $\mathbf{a}_1 = (x_1, y_1)$, $\mathbf{a}_2 = (x_2, y_2)$, $\mathbf{a}_3 = (x_3, y_3)$:

1. Compute area: $|K| = \frac{1}{2}|(x_2-x_1)(y_3-y_1) - (x_3-x_1)(y_2-y_1)|$
2. Compute edge vectors: $\mathbf{e}_{12} = \mathbf{a}_2 - \mathbf{a}_1$, $\mathbf{e}_{13} = \mathbf{a}_3 - \mathbf{a}_1$
3. Form $\mathbf{B}_K = (\mathbf{e}_{12}\;|\;\mathbf{e}_{13})$, compute $\mathbf{B}_K^{-T}$
4. Gradient matrix: $\mathbf{G}_K \in \mathbb{R}^{2\times 3}$ from the $3\times 3$ system (Eq. 2.4.5.10), columns = $\nabla\lambda_i$
5. Element stiffness: $\mathbf{A}_K = |K|\,\mathbf{G}_K^T\,\mathbf{G}_K$
6. Element mass: $\mathbf{M}_K = \frac{|K|}{12}(\mathbf{I} + \mathbf{1}\mathbf{1}^T)$

### Recipe 3: Assemble global matrix from element matrices

1. Initialize global matrix $\mathbf{A}$ as zero (sparse)
2. For each cell $K$: get local-to-global DOF map $\{i_1, i_2, i_3\}$
3. Compute element matrix $\mathbf{A}_K$
4. For each pair $(l,m) \in \{1,2,3\}^2$: $\mathbf{A}[i_l, i_m] \mathrel{+}= (\mathbf{A}_K)_{lm}$

---

## Homework Problems

> [[FEM-1D-2D-Problems]]

| Problem | Title | Code folder | Key skills |
|---------|-------|-------------|------------|
| **2-1** | Properties of Galerkin Solutions | — | Galerkin orthogonality, best approximation |
| **2-2** | Transformation of Galerkin Matrices | `TransformationOfGalerkinMatrices` | Basis change, conditioning |
| **2-3** | Pointwise "Exact" Galerkin Solution | — | Superconvergence at nodes |
| **2-4** | Linear FE for Two-Point BVP | `LinearFE1D` | Full 1D FEM pipeline |
| **2-5** | Triangular Linear FEM for 2D Reaction-Diffusion | `SimpleLinearFiniteElements` | Full 2D pipeline |
| **2-10** | Projection onto Gradients | `ProjectionOntoGradients` | Custom bilinear form |
| **2-11** | Hybrid-Mesh Galerkin Matrices | — | Mixed triangle/quad meshes |

---

## Exam Problems

> Full bank: [[Exam-Master-Bank#Ch2]] | Hub: [[Exam-Prep-Index]]

| Year | Exam | Problem | Topic | HW / note |
|------|------|---------|-------|-----------|
| **2026** | Midterm | 0-3 | Quadratic Lagrangian Finite Element Method | 2-20 QuadLagrFEM |
| **2026** | Midterm | 0-2 | Element Matrix on a Curved Triangle | 2-13 ElementMatrixCurvedTriangle; [[Exam-Deep-Element-Matrices]] |
| **2023** | Midterm | 0-3 | DofHandler and Assembly | 2-20 DOFHandlerAssembly |
| **2023** | Midterm | 0-2 | Lagrangian Finite Elements on Criss-Cross Meshes | 2-19 FESpacesCrissCross; [[Exam-Deep-Element-Matrices]] |
| **2022** | Midterm | 0-3 | Sparsity of Galerkin matrices | — — |
| **2022** | Endterm | 0-1 | Finite-Volume Method/Finite-Difference Method on T… | — — |
| **2021** | Final (Summer) | 1-1 | Non-conforming Crouzeix-Raviart FEM: Theoretical a… | — — |
| **2019** | Midterm | 0-3 | Operating locally on Galerkin matrices | — — |
| **2019** | Midterm | 0-2 | Cubic Lagrangian finite element space on 2D hybrid… | — — |

---

## Connections

| This week | Builds on | Feeds into |
|-----------|-----------|------------|
| Galerkin discretization | [[Week-01-Elliptic-BVPs-I]] (Lax-Milgram) | [[Week-04-FEM-II]] (assembly in LehrFEM++) |
| 1D tent functions | — | [[Week-07-Parabolic-IBVPs]] (1D MOL) |
| 2D element matrices | [[Week-02-Elliptic-BVPs-II]] (variational form) | [[Week-07-Parabolic-IBVPs]] ($\mathbf{M}$, $\mathbf{A}$ in MOL ODE) |
| Galerkin orthogonality | — | [[Galerkin-Orthogonality]] → [[Week-05-Parametric-FEM-and-Error]] ([[Cea-Lemma]]) |

---

## Exam Checklist

- [ ] Compute element stiffness and mass for a 1D interval (given $h$, $\alpha(x)$)
- [ ] Compute element stiffness and mass for a 2D triangle (given vertices)
- [ ] Compute barycentric coordinate gradients from vertex coordinates
- [ ] Assemble a small global matrix from element contributions (by hand, 3–4 elements)
- [ ] State Galerkin orthogonality and the best approximation property
- [ ] Explain why Galerkin matrix is sparse (local support of basis functions)
