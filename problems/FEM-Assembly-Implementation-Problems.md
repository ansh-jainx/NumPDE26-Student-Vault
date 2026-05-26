---
tags: [problems, chapter-2, LehrFEM, assembly, implementation, mesh]
---

# FEM Assembly & Implementation Problems

Problems from Chapter 2 covering §2.7: mesh data structures, DOF handling, cell-oriented assembly, local computations, essential BC treatment, parametric FEM — all using LehrFEM++.

---

## Problem 2-6: Incidence Matrices of a Hybrid 2D Mesh

**Code folder:** `IncidenceMatrices` | **Sections:** §2.7.1–§2.7.2

**Concepts:** [[Mesh-Data-Structures]]

**Setup:** Build incidence matrices (node-edge, edge-cell) from a LehrFEM++ mesh object. Navigate mesh topology using `Entity` and co-dimension queries.

| What it tests |
|--------------|
| `lf::mesh::Mesh`, `lf::mesh::Entity` |
| Incidence relations, co-dimension concept |
| Sparse matrix construction from mesh topology |

> [!abstract] Solution gist
> Iterate cells (`mesh_p->Entities(0)`), for each cell get sub-entities: edges via `cell.SubEntities(1)`, nodes via `cell.SubEntities(2)`. Build node-edge and edge-cell incidence matrices as sparse $\{0,1\}$-matrices. Use `mesh_p->Index(*entity)` for matrix row/column indices. Orientation can be tracked via local sub-entity numbering.

---

## Problem 2-7: Computing the Length of the Boundary in LehrFEM++

**Code folder:** `LengthOfBoundary` | **Sections:** §2.7.1

**Concepts:** [[Mesh-Data-Structures]]

**Setup:** Loop over boundary edges of a mesh and sum their lengths. Introduction to `lf::geometry::Volume()` and boundary detection.

| What it tests |
|--------------|
| Iterating over mesh entities |
| Boundary detection: `flagEntitiesOnBoundary` |
| `lf::geometry::Volume()` for edge length / cell area |

> [!abstract] Solution gist
> `auto bd_flags = lf::mesh::utils::flagEntitiesOnBoundary(mesh_p);` Then: `for (auto* edge : mesh_p->Entities(1)) { if (bd_flags(*edge)) total += lf::geometry::Volume(*edge->Geometry()); }`. `Volume()` returns length for 1D entities (edges) and area for 2D entities (cells).

---

## Problem 2-8: Introduction to Local Assembly in LehrFEM++

**Code folder:** `ElementMatrixComputation` | **Sections:** §2.7.4–§2.7.5

**Concepts:** [[Assembly-Algorithm]], [[Local-Computations]]

**Setup:** Implement a custom `EntityMatrixProvider` that computes element stiffness matrices. First contact with the assembly interface.

| What it tests |
|--------------|
| Writing a custom element matrix provider |
| `AssembleMatrixLocally()` API |
| Local-to-global DOF mapping |

> [!tip] Template for all later problems
> This is the pattern used in every LehrFEM++ problem from Ch9 onward (Problems 9-1, 9-2, etc.). Master this one first.

> [!abstract] Solution gist
> Write class with `bool isActive(const Entity&)` and `Eigen::MatrixXd Eval(const Entity& cell)`. In `Eval`: get geometry → corners → compute gradients $\nabla\lambda_i$ → element stiffness $|K|\nabla\lambda_i \cdot \nabla\lambda_j$. Then: `COOMatrix<double> A(N,N); AssembleMatrixLocally(0, dofh, dofh, provider, A);`. The assembly function calls `Eval` for each cell and scatters entries using `dofh.GlobalDofIndices(cell)`.

---

## Problem 2-9: Handling Degrees of Freedom (DOFs) in LehrFEM++

**Code folder:** `LFPPDofHandling` | **Sections:** §2.7.3

**Concepts:** [[Mesh-Data-Structures]], [[Assembly-Algorithm]]

**Setup:** Explore the `UniformFEDofHandler`: query DOFs per entity type, local↔global mappings, DOF locations.

| What it tests |
|--------------|
| `lf::assemble::UniformFEDofHandler` |
| DOF distribution for $p=1$ and $p=2$ |
| Local-to-global index mapping |

> [!abstract] Solution gist
> Explore `dofh.NumDofs()` (total), `dofh.GlobalDofIndices(entity)` (local→global for a cell), `dofh.InteriorGlobalDofIndices(entity)` (DOFs owned by entity). For $p=1$: 1 DOF per node, 0 per edge, 0 per cell → $N = \#\text{nodes}$. For $p=2$: 1 per node + 1 per edge → $N = \#\text{nodes} + \#\text{edges}$. `dofh.Entity(dof_idx)` gives the mesh entity owning a DOF.

---

## Problem 2-12: Testing Built-In Quadrature Rules of LehrFEM++

**Code folder:** `TestQuadratureRules` | **Sections:** §2.7.5

**Concepts:** [[Local-Computations]]

**Setup:** Verify quadrature rules by integrating known polynomials. Check exactness order.

| What it tests |
|--------------|
| `lf::quad` module |
| Quadrature rule selection and verification |

> [!abstract] Solution gist
> `auto qr = lf::quad::make_QuadRule(lf::base::RefEl::kTria(), order);` Verify by integrating monomials $x^a y^b$ with $a+b \leq \text{order}$: compare `sum(wts[l] * f(pts.col(l)) * int_el[l])` against exact integral. A rule of order $p$ must integrate polynomials of degree $\leq p$ exactly. Check that errors are near machine epsilon for in-range degrees and grow for higher degrees.

---

## Problem 2-13: Local Computations for Parametric Lagrangian FE

**Code folder:** `ParametricElementMatrices` | **Sections:** §2.7.5, §2.7.7

**Concepts:** [[Local-Computations]], [[Parametric-FEM]]

> [!warning] Exam alert
> **2026 Midterm 0-2** (`ElementMatrixCurvedTriangle`). Strategy: [[Exam-Deep-Element-Matrices]].

**Setup:** Compute element matrices for higher-order (parametric) elements using reference element + quadrature. Gradient transformation via Jacobian.

| What it tests |
|--------------|
| Reference element computations (Lemma 2.8.3.10) |
| Jacobian-based gradient transformation |
| Quadrature on reference element |
| Parametric vs affine elements |

> [!abstract] Solution gist
> On reference element $\hat{K}$: evaluate shape functions $\hat{b}_i(\hat{\mathbf{x}})$ and their gradients $\hat{\nabla}\hat{b}_i$ at quadrature points. Transform: $\nabla b_i = \mathbf{F}_K^{-\top}\hat{\nabla}\hat{b}_i$ (Lemma 2.8.3.10). Element stiffness: $(\mathbf{A}_K)_{ij} = \sum_l w_l\,(\mathbf{F}_K^{-\top}\hat{\nabla}\hat{b}_i)^\top(\mathbf{F}_K^{-\top}\hat{\nabla}\hat{b}_j)\,|\det\mathbf{F}_K|\bigg|_{\hat{\mathbf{x}}_l}$. For affine elements $\mathbf{F}_K$ is constant; for parametric (curved) elements, evaluate $\mathbf{F}_K(\hat{\mathbf{x}}_l)$ at each quadrature point via `geo->Jacobian(pts)`.

---

## Problem 2-14: Non-Conforming Crouzeix-Raviart FEM

**Code folder:** `NonConformingCrouzeixRaviartFiniteElements` | **Sections:** §2.5, §2.7

**Concepts:** [[Lagrangian-FEM]]

**Setup:** Implement FEM with DOFs at edge midpoints (non-conforming: $V_h \not\subset H^1$). Full pipeline: element matrices, assembly, BC treatment, convergence.

| What it tests |
|--------------|
| Non-conforming FE spaces |
| Edge-based DOFs |
| Full LehrFEM++ pipeline for a non-standard element |

> [!abstract] Solution gist
> Crouzeix-Raviart: DOFs at edge midpoints, basis functions $b_e(\mathbf{x})$ piecewise linear but discontinuous across edges ($V_h \not\subset H^1$). On reference triangle: 3 shape functions associated with midpoints of the 3 edges. Element stiffness same formula as conforming linear FEM (same gradients on each cell). Assembly uses edge-based DOF handler. BCs: flag boundary edge DOFs. Non-conforming → Galerkin orthogonality holds only in a modified sense, but convergence rates match conforming $p=1$ FEM.

---

## Problem 2-15: Regularized Neumann Problem

**Code folder:** `RegularizedNeumannProblem` | **Sections:** §2.7.6

**Concepts:** [[Essential-BC-Treatment]], [[Boundary-Conditions-Elliptic]]

**Setup:** Pure Neumann problem (no Dirichlet BC). Singular system — regularize by adding constraint $\int_\Omega u = 0$ via Lagrange multiplier or penalty.

| What it tests |
|--------------|
| Singular Galerkin matrix (pure Neumann) |
| Regularization techniques |
| Constraint enforcement |

> [!warning] Common mistake
> Pure Neumann: the stiffness matrix $\mathbf{A}$ has a null space (constant vector). Must either fix one DOF or add a mean-value constraint.

> [!abstract] Solution gist
> Pure Neumann: $\mathbf{A}\boldsymbol{\mu} = \boldsymbol{\phi}$ is singular ($\ker\mathbf{A} = \text{span}(\mathbf{1})$). Solution exists iff $\mathbf{1}^\top\boldsymbol{\phi} = 0$ (compatibility). Regularization options: (1) Fix one DOF ($\mu_1 = 0$) → modify row/column 1. (2) Lagrange multiplier: augmented system $\begin{pmatrix}\mathbf{A} & \mathbf{1}\\\mathbf{1}^\top & 0\end{pmatrix}\begin{pmatrix}\boldsymbol{\mu}\\\lambda\end{pmatrix} = \begin{pmatrix}\boldsymbol{\phi}\\0\end{pmatrix}$. (3) Penalty: $\mathbf{A} + \epsilon\mathbf{M}$ with small $\epsilon$. Option (2) enforces $\int u_h = 0$ exactly.

---

## Problem 2-17: Local Computations for Convection Bilinear Form

**Code folder:** `ConvBLFMatrixProvider` | **Sections:** §2.7.5

**Concepts:** [[Local-Computations]], [[Assembly-Algorithm]], [[Upwind-Quadrature]]

**Setup:** Implement element matrix provider for the convection term $\int_K (\mathbf{v} \cdot \nabla u)\,w\,\mathrm{d}\mathbf{x}$. Non-symmetric bilinear form.

| What it tests |
|--------------|
| Non-symmetric element matrices |
| Convection term assembly |
| Continuous form before [[Streamline-Diffusion]] / upwind (Ch 10) |

> [!abstract] Solution gist
> Element matrix for $\int_K (\mathbf{v}\cdot\nabla u)\,w$: non-symmetric! On triangle $K$ with constant $\mathbf{v}$: $(\mathbf{C}_K)_{ij} = |K|\,(\mathbf{v} \cdot \nabla\lambda_j)\,\bar{\lambda}_i$ where $\bar{\lambda}_i = 1/3$ (barycentric mean). For variable $\mathbf{v}$: use quadrature. The provider `Eval` returns a non-symmetric $n_\text{loc} \times n_\text{loc}$ matrix. Key: `AssembleMatrixLocally` doesn't require symmetry.

---

## Problem 2-18: Nitsche's Method for Elliptic BVPs

**Sections:** §2.7.6

**Concepts:** [[Essential-BC-Treatment]]

**Setup:** Alternative to strong BC enforcement: Nitsche's method imposes Dirichlet BCs weakly via penalty + consistency terms. Implement and test convergence.

| What it tests |
|--------------|
| Weak enforcement of essential BCs |
| Nitsche penalty parameter selection |

> [!abstract] Solution gist
> Nitsche's method: instead of strongly imposing $u = g$ on $\Gamma_D$, add penalty + consistency terms to the bilinear form: $a_h(u,v) = \int_\Omega \nabla u \cdot \nabla v - \int_{\Gamma_D}(\nabla u \cdot \mathbf{n})v - \int_{\Gamma_D}(\nabla v \cdot \mathbf{n})u + \frac{\eta}{h}\int_{\Gamma_D} uv$. Penalty $\eta/h$ must be large enough for coercivity ($\eta > C_\text{inv}$). Consistency terms ensure optimal convergence. Assembles as: stiffness + two boundary terms (edge-based) + penalty edge mass. No modification of rows/columns needed (weak BCs).

---

## Problem 2-20: DofHandler and Assembly

**Code folder:** `LFPPDofHandling` | **Sections:** §2.7.3–§2.7.4

> Midterm exam PDFs may use `DOFHandlerAssembly` or `QuadLagrFEM` — both map to this folder.

**Concepts:** [[Assembly-Algorithm]], [[Mesh-Data-Structures]], [[Lagrangian-FEM]]

> [!warning] Exam alert
> **2023 Midterm 0-3** / **2026 Midterm 0-3** (DOFHandler, quadratic FEM). See [[Exam-Master-Bank#Ch2]].

**Setup:** Comprehensive exercise on DOF handling and assembly with different polynomial degrees and entity types.

| What it tests |
|--------------|
| DOF handler for mixed-order elements |
| Assembly with higher-order FE spaces |

> [!abstract] Solution gist
> Practice combining `FeSpaceLagrangeO1` and `FeSpaceLagrangeO2` DOF handlers. For $p=2$: DOFs at nodes AND edge midpoints. `dofh.GlobalDofIndices(cell)` returns 6 indices (3 nodes + 3 edges) for a triangle. Element matrices are $6\times 6$. Assembly is identical — `AssembleMatrixLocally` is degree-agnostic, the provider handles the local dimension.

---

## Problem 2-21: Blended Parametric Representation of Curvilinear Triangles

**Code folder:** `BlendedParameterization` | **Sections:** §2.7.7

**Concepts:** [[Parametric-FEM]], [[Local-Computations]]

**Setup:** Implement blended parametric maps for triangles with one curved edge. Used for domains with curved boundaries.

| What it tests |
|--------------|
| Parametric geometry representations |
| Blended maps (linear + curved correction) |

> [!abstract] Solution gist
> For domains with one curved edge: $\Phi_K(\hat{\mathbf{x}}) = \Phi_K^{\text{affine}}(\hat{\mathbf{x}}) + \text{blending correction}$. The blending function is non-zero only near the curved edge and vanishes at straight edges. This makes the Jacobian $\mathbf{F}_K$ non-constant → need quadrature for element matrices. Implement as a custom `lf::geometry::Geometry` subclass or use LehrFEM++'s built-in parametric geometry.

---

## Problem 2-22: Constrained Neumann Problem

**Code folder:** `SolAvgBoundary` | **Sections:** §2.7.6

**Concepts:** [[Boundary-Conditions-Elliptic]], [[Stokes-Saddle-Point]]

**Setup:** Neumann problem with constraint on boundary average of solution. Saddle-point system.

| What it tests |
|--------------|
| Constrained optimization / saddle point |
| Lagrange multiplier technique |
| Preview: [[Stokes-Saddle-Point]] and [[LBB-Condition]] (Ch 12) |

> [!abstract] Solution gist
> Neumann problem with constraint $\int_{\partial\Omega} u\,\mathrm{d}S = c$. Saddle-point system: $\begin{pmatrix}\mathbf{A} & \mathbf{b}\\\mathbf{b}^\top & 0\end{pmatrix}\begin{pmatrix}\boldsymbol{\mu}\\\lambda\end{pmatrix} = \begin{pmatrix}\boldsymbol{\phi}\\c\end{pmatrix}$, where $b_i = \int_{\partial\Omega} b_i^h\,\mathrm{d}S$ (boundary integrals of basis functions). Lagrange multiplier $\lambda$ enforces the constraint. Well-posedness requires $\mathbf{b} \notin \text{range}(\mathbf{A})$ → satisfied since $\mathbf{A}$ kernel is constants and $\mathbf{b}^\top\mathbf{1} = |\partial\Omega| \neq 0$. Preview of the LBB condition from Ch12.

---

## Problem 2-24: Parametric FEM: Local Computations

**Code folder:** `ParametricElementMatrices` | **Sections:** §2.7.5, §2.7.7

**Concepts:** [[Parametric-FEM]], [[Local-Computations]]

**Setup:** Element matrix computation for parametric (curved) elements with quadrature. Full local computation pipeline.

| What it tests |
|--------------|
| Complete parametric FEM local computation |
| Quadrature on curved elements |

> [!abstract] Solution gist
> Combines 2-13 and 2-21: parametric element with non-constant Jacobian. Full pipeline: (1) Get quadrature rule for reference element. (2) Evaluate shape functions and gradients at quadrature points on $\hat{K}$. (3) For each point: compute $\mathbf{F}_K = $ `geo->Jacobian(pt)`, transform gradients via $\nabla b_i = \mathbf{F}_K^{-\top}\hat{\nabla}\hat{b}_i$. (4) Weight by $|\det\mathbf{F}_K|$ = `geo->IntegrationElement(pt)` and quadrature weight. (5) Sum contributions into element matrix.

---

**Exams:** Midterm 0-2 and 0-3 (most years) test assembly concepts from these problems.

---

**Related concepts:** [[Lagrangian-FEM]], [[Mesh-Data-Structures]], [[Assembly-Algorithm]], [[Local-Computations]], [[Essential-BC-Treatment]], [[Parametric-FEM]], [[LehrFEM-Assembly-Patterns]], [[LehrFEM-Mesh-Patterns]], [[Formulas-FEM-Assembly]]
