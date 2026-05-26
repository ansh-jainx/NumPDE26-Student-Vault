---
tags: [exam, exam-critical, chapter-2, deep-dive]
---

# Exam Deep Dive — Element Matrices

**Theme:** Local stiffness/ mass on curved or macro meshes (3×) | **Type C** | **HW:** 2-13, 2-19

> Master bank: [[Exam-Master-Bank#Ch2]] | Weeks: [[Week-03-FEM-I]], [[Week-04-FEM-II]]

---

## Anchor exams

| Year | Exam | Problem | Title | Folder | HW |
|------|------|---------|-------|--------|-----|
| 2026 | Midterm | 0-2 | Element matrix on curved triangle | `ElementMatrixCurvedTriangle` | 2-13 |
| 2023 | Midterm | 0-2 | Lagrangian FE on criss-cross meshes | `FESpacesCrissCross` | 2-19 |

Related: 2024 Midterm convection BLF → [[Exam-Deep-Convection-Upwind]] (same local assembly skill).

---

## Curved triangle (2026 0-2)

**Strategy:**
1. Parametric map $F_K: \widehat{K} \to K$; $J = DF_K$.
2. $\int_K \nabla u\cdot\nabla v = \int_{\widehat{K}} \hat{\nabla}\hat{u}\, G^{-1}\,\hat{\nabla}\hat{v}\,|J|\,\mathrm{d}\xi$ with $G = J^TJ$.
3. Quadrature on reference triangle; per-element loop.
4. **Variational crime:** geometry approximation vs exact domain (link [[Variational-Crimes]]).

**HW:** [[FEM-Assembly-Implementation-Problems#Problem 2-13]] | Exam PDF folder: `ElementMatrixCurvedTriangle` → NPDERepo: `homeworks/ParametricElementMatrices`.

---

## Criss-cross (2023 0-2)

**Strategy:**
1. Macro-element split into 4 sub-triangles; non-standard DOF layout.
2. Continuity constraints — which DOFs are shared vs interior bubble.
3. Assembly on sub-cells; global DOF handler merges contributions.

**HW:** Problem **2-19** | Repo: `FESpacesCrissCross`.

---

## Local computation checklist

- [ ] Reference vs physical gradients (Piola not needed for scalar $H^1$)
- [ ] Quadrature order sufficient for $P_p$ on curved geometry
- [ ] Symmetry of diffusion stiffness; **not** for convection
- [ ] `AssembleMatrixLocally(codim, ...)` — codim 0 for volume

---

## Links

- [[Local-Computations]], [[Parametric-FEM]], [[Assembly-Algorithm]]
- [[FEM-Assembly-Implementation-Problems]]
- [[LehrFEM-Assembly-Patterns]]
