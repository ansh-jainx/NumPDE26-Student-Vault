---
tags: [week-11, chapter-13, FEEC, differential-forms, exterior-calculus, exam-critical]
---

# Week 11 — FEEC I: Forms and Exterior Calculus

**Sections:** §13.1.1–§13.1.5 | **Chapter 13: Finite-Element Exterior Calculus (foundations)**

---

## Overview

This week starts FEEC with the language needed for computational electromagnetism: [[Differential-Forms]], [[Exterior-Derivative-and-de-Rham-Complex]], and [[Sobolev-Spaces-of-Forms]]. Core message: keep geometry/topology in the operators and put material laws in bilinear forms. This structure is the basis for [[Whitney-Forms]] in Week 12 and stable magnetostatics in Week 13. Formula sheet: [[Formulas-Exterior-Calculus]].

```mermaid
graph LR
    A[Fields and Integrals] --> B[Differential Forms]
    B --> C[Exterior Derivative d]
    C --> D[de Rham Complex]
    D --> E[Sobolev Spaces of Forms]
    E --> F[FE Discretization in Week 12]
    style F fill:#f96
```

---

## Theory Gist

### §13.1.1–§13.1.3 — Fields, integral forms, differential forms

See [[Differential-Forms]].

Forms unify scalar and vector field viewpoints through integration over geometric entities of matching dimension.

> [!info] Structural view
> Unknowns are not just component vectors; they are $\ell$-forms tied to edges/faces/volumes via integration.

### §13.1.4.2 — Exterior derivative

See [[Exterior-Derivative-and-de-Rham-Complex]].

$$d^{\ell+1}d^\ell = 0$$

This is the abstract source of identities like $\mathrm{curl}\,\nabla=0$ and $\mathrm{div}\,\mathrm{curl}=0$.

### §13.1.4.3 — Potentials

Potential formulations arise from kernel-image relations in the de Rham sequence. This is the bridge to magnetostatics in Week 13.

### §13.1.5 — Sobolev spaces of forms

See [[Sobolev-Spaces-of-Forms]].

Choose spaces compatible with the derivative in the model:

- $H^1$ for gradients,
- $H(\mathrm{curl})$ for curl fields,
- $H(\mathrm{div})$ for flux fields.

> [!warning] Wrong conformity
> Choosing scalar $H^1$ spaces for inherently $H(\mathrm{curl})$ unknowns breaks the Maxwell structure and can cause spurious modes.

---

## Method Recipes

### Recipe 1: Translate vector PDE notation into form notation

1. Identify physical quantity (potential, field, flux) and associated form degree
2. Replace grad/curl/div chain with $d^\ell$ operators
3. Verify compatibility identity $d^{\ell+1}d^\ell=0$

### Recipe 2: Select variational spaces by operator chain

1. Start from strongest derivative in the PDE
2. Assign Sobolev-of-forms space where that derivative is weakly defined
3. Check boundary traces (tangential vs normal) for BCs

### Recipe 3: Detect potential formulations

1. Check whether field is constrained by derivative-free condition (e.g. closed form)
2. Use de Rham exactness intuition to introduce potential variable
3. Track gauge/non-uniqueness early for later mixed formulations

---

## Homework Problems

> [[FEEC-EM-Waves-Problems]]

| Problem | Title | Code folder | Key skills |
|---------|-------|-------------|------------|
| **13-1** | Incidence Matrices of a 2D Finite Element Mesh | `IncidenceMatrices` | Preview of Week 12 discrete operators |

---

## Exam Problems

> Full bank: [[Exam-Master-Bank#Ch13]] | Hub: [[Exam-Prep-Index]]

| Year | Exam | Problem | Topic | HW / note |
|------|------|---------|-------|-----------|
| **2025** | Final (Summer) | 1-3 | Whitney Finite Elements for Magnetostatic BVP in T… | 13-3 MagStat2D; [[Exam-Deep-FEEC-Maxwell]] |
| **2025** | Final (Winter) | 1-3 | TM-Mode Electromagnetic Wave Equation | 13-4 MaxwellEvlTM; [[Exam-Deep-FEEC-Maxwell]] |

---

## Connections

| This week | Builds on | Feeds into |
|-----------|-----------|------------|
| Form language for PDEs | [[Week-02-Elliptic-BVPs-II]], [[Week-03-FEM-I]] | [[Week-12-FEEC-II-and-EM-Waves]] |
| Operator chain and exactness | [[Linear-Variational-Problem]] | [[Cochain-Calculus]], [[Whitney-Forms]] |
| Sobolev spaces of forms | [[Sobolev-Spaces]] | [[Electromagnetic-Wave-Equations]], [[Week-13-FEEC-Magnetostatics]] |

---

## Exam Checklist

- [ ] Explain form degree interpretation (0/1/2/3-forms in 3D proxies)
- [ ] State and use $d^{\ell+1}d^\ell=0$
- [ ] Reconstruct grad/curl/div chain as de Rham complex
- [ ] Choose correct Sobolev-of-forms space for a Maxwell-type field
- [ ] Explain why compatibility identities matter for discretization stability
- [ ] Connect potential formulations to exactness intuition
