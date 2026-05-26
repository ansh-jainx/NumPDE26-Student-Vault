---
tags: [problems, chapter-13, FEEC, Maxwell, waves]
---

# FEEC and EM Waves Problems

Problems from Chapter 13 focusing on discrete forms, cochains, and electromagnetic wave evolution.

---

## Problem 13-1: Incidence Matrices of a 2D Finite Element Mesh

**Code folder:** `IncidenceMatrices` | **Sections:** §13.2.1.1–§13.2.1.2

**Concepts:** [[Cochain-Calculus]], [[Discrete-Exterior-Derivative]], [[Differential-Forms]]

**Setup:** Build oriented incidence matrices on simplicial meshes and verify algebraic identities corresponding to discrete exterior calculus.

| Sub-task | What it asks |
|----------|--------------|
| (a) | Define oriented facets and cochain indexing |
| (b) | Construct edge-vertex and face-edge incidence matrices |
| (c) | Verify composition identity $\mathbf D_1\mathbf D_0 = 0$ |

> [!abstract] Solution gist
> Incidence entries are $\{-1,0,1\}$ from orientation. Matrix products encode boundary-of-boundary equals zero, the discrete analog of $d^{\ell+1}d^\ell=0$.

> [!warning] Common mistake
> Inconsistent facet orientation breaks exactness checks and produces non-zero $\mathbf D_1\mathbf D_0$.

---

## Problem 13-4: TM-Mode Electromagnetic Wave Equation

**Code folder:** `MaxwellEvlTM` | **Sections:** §13.3.2.1–§13.3.2.3

> NPDERepo path: `developers/MaxwellEvlTM/mysolution/`

**Concepts:** [[Electromagnetic-Wave-Equations]], [[Whitney-Forms]], [[Cochain-Calculus]], [[Method-of-Lines]]

> [!warning] Exam alert
> **2025 Winter Final 1-3** (`MaxwellEvlTM`). Deep dive: [[Exam-Deep-FEEC-Maxwell#MaxwellEvlTM (HW 13-4) — Winter]].

**Setup:** Variational and semi-discrete treatment of TM-mode Maxwell wave equations with FEEC-compatible spaces and timestepping.

| Sub-task | What it asks |
|----------|--------------|
| (a) | Derive wave evolution variational equations |
| (b) | Build semi-discrete matrix system from Whitney spaces |
| (c) | Analyze constraint propagation and energy behavior |
| (d+) | Implement timestepping and test on benchmark domain |

> [!abstract] Solution gist
> Use form-degree matched spaces; assemble mass/curl coupling blocks; evolve with implicit or structure-preserving timestepping. Preserve divergence constraints through compatible discrete operators.

> [!warning] Common mistake
> Replacing edge-based FE spaces by scalar nodal spaces destroys $H(\mathrm{curl})$ conformity and yields nonphysical wave modes.

---

**Related concepts:** [[Differential-Forms]], [[Cochain-Calculus]], [[Discrete-Exterior-Derivative]], [[Whitney-Forms]], [[Electromagnetic-Wave-Equations]], [[Formulas-Exterior-Calculus]], [[LehrFEM-FEEC-Patterns]]
