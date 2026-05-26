---
tags: [exam, exam-critical, midterm, exam-bank]
---

# Midterm Compendium (2021–2026)

Tier **B** summaries for every midterm problem. Anchor strategies: [[Exam-Deep-Elliptic-Weak-Form]], [[Exam-Deep-Convergence-Plots]], [[Exam-Deep-Element-Matrices]], [[Exam-Deep-Convection-Upwind]].

Sources: `NPDE21_Midterm_sols.pdf` … `NPDE26_Midterm_sols.pdf`, `NPDE_Midterm_Spring_2019_sols.pdf`.

---

## Recurring structure

| Slot | Typical topic | Deep dive |
|------|---------------|-----------|
| **0-1** | Elliptic BVP ↔ variational form | [[Exam-Deep-Elliptic-Weak-Form]] |
| **0-2** | Convergence plots **or** element matrix / mesh | [[Exam-Deep-Convergence-Plots]] / [[Exam-Deep-Element-Matrices]] |
| **0-3** | Convection BLF **or** DOFHandler / quadratic FEM | [[Exam-Deep-Convection-Upwind]] / [[Week-04-FEM-II]] |

Full table: [[Exam-Master-Bank#Ch1]], [[Exam-Master-Bank#Ch2]], [[Exam-Master-Bank#Ch3]].

---

## 2026 Midterm

### 0-1 — Reformulating elliptic variational problem
**Type A/B** | HW **1-10**, **1-11** | Folder: `VPtoBVP` (when coding variant appears)

**Strategy:** Given strong or weak form, derive the dual formulation; classify Dirichlet/Neumann/Robin; state coercivity space. Mixed BCs are the twist vs 2023.

→ [[Exam-Deep-Elliptic-Weak-Form#2026 Midterm 0-1]]

### 0-2 — Element matrix on curved triangle
**Type C** | HW **2-13** | Exam PDF: `ElementMatrixCurvedTriangle` → NPDERepo: `homeworks/ParametricElementMatrices`

**Strategy:** Parametric map $F_K$; pull back stiffness to $\widehat{K}$; $|J|$ and $\hat{\nabla}$ transform; quadrature on reference triangle.

→ [[Exam-Deep-Element-Matrices]]

### 0-3 — Quadratic Lagrangian FEM
**Type C/G** | HW **2-20** | Exam PDF: `DOFHandlerAssembly` / `QuadLagrFEM` → NPDERepo: `homeworks/LFPPDofHandling`

**Strategy:** DOF count on triangle ($P_2$ has 6 DOFs); sparsity pattern; assembly loop structure; essential BC on boundary DOFs.

---

## 2024 Midterm

### 0-1 — Galerkin convection bilinear form
**Type C** | HW **2-17** | Exam PDF: `ConvectionBilinearForm` → NPDERepo: `homeworks/ConvBLFMatrixProvider`

**Strategy:** Local matrix $\int_K \mathbf{b}\cdot\nabla \phi_j\,\phi_i$; non-symmetric; compare to diffusion stiffness.

→ [[Exam-Deep-Convection-Upwind#2024 Midterm 0-1]]

### 0-2 — (See exam PDF — assembly / FEM topic)
Check `NPDE24_Midterm_sols.pdf` Problem 0-2 in [[Exam-Master-Bank]].

### 0-3 — (See exam PDF)
Listed in master bank Ch.2/Ch.3.

---

## 2023 Midterm

### 0-1 — BVP → variational problems
**Type A** | HW **1-10**

**Strategy:** Same elliptic chain as 2021/2022; emphasize fundamental lemma recovery.

→ [[Exam-Deep-Elliptic-Weak-Form#2023 Midterm 0-1]]

### 0-2 — Lagrangian FE on criss-cross meshes
**Type C/E** | HW **2-19** | Folder: `FESpacesCrissCross`

**Strategy:** Non-conforming or macro-element spaces on criss-cross partition; DOF location; continuity constraints across sub-triangles.

→ [[Exam-Deep-Element-Matrices#Criss-cross]]

### 0-3 — DofHandler and assembly
**Type G** | HW **2-20** | Exam PDF: `DOFHandlerAssembly` → NPDERepo: `homeworks/LFPPDofHandling`

**Strategy:** `DofHandler` layout; `AssembleMatrixLocally`; sparsity from mesh connectivity.

---

## 2022 Midterm

### 0-1 — BVP, variational form, quadratic minimization
**Type A** | HW **1-1**, **1-10**

**Strategy:** Derive weak form; show equivalence to minimization of energy functional.

→ [[Exam-Deep-Elliptic-Weak-Form]]

### 0-2 — Galerkin FEM for advection bilinear form
**Type C** | HW **2-17**

→ [[Exam-Deep-Convection-Upwind]]

### 0-3 — (Convection local computations — see PDF)
Linked to 2-17 in [[Week-03-FEM-I]] exam table.

---

## 2021 Midterm

### 0-1 — Second-order elliptic BVP from weak formulations
**Type A** | HW **1-9**

→ [[Exam-Deep-Elliptic-Weak-Form#2021 Midterm 0-1]]

### 0-2 — Asymptotic convergence of FE and interpolation errors
**Type F** | HW **3-15**

**Strategy:** Log-log slopes; $h^p$ for $H^1$; distinguish $u - u_h$ vs $u - I_h u$.

→ [[Exam-Deep-Convergence-Plots#2021 Midterm 0-2]]

### 0-3 — Local computations for convection bilinear form
**Type C** | HW **2-17**

→ [[Exam-Deep-Convection-Upwind]]

---

## 2019 Midterm (legacy)

Tier **C** in master bank — Ch.1–2 topics predating current week numbering. Spot-check PDF before relying on HW mapping.

---

## Study checklist

- [ ] Can derive midterm 0-1 from strong BVP without notes (Type A)
- [ ] Can read convergence plot and state order ±0.1 (Type F)
- [ ] Can write element stiffness on reference triangle (Type C)
- [ ] Know `ConvectionBilinearForm` vs diffusion sign / symmetry

**Next:** Endterm scope → [[Endterm-Prep-Ch9-Ch12]]; coding finals → [[Finals-Compendium]].
