---
tags: [chapter-13, FEEC, cochains, discrete-forms]
first_appears: "[[Week-12-FEEC-II-and-EM-Waves]]"
---

# Cochain Calculus

**Reference:** §13.2.1

---

## Discrete counterpart of forms

On an oriented mesh $\mathcal{M}$, an $\ell$-cochain stores one scalar per $\ell$-facet.

- 0-cochains: vertex values
- 1-cochains: edge circulations
- 2-cochains: face fluxes

Incidence matrices encode mesh topology and implement discrete exterior derivatives.

> [!info] Topological operator
> Cochain derivatives depend only on orientation and incidence, not on metric material data.

## Why this matters

Cochain equations give algebraic Maxwell systems that preserve exact identities from the continuous theory.

---

**Problems:** 13-1 | **Related:** [[Discrete-Exterior-Derivative]], [[Whitney-Forms]], [[Differential-Forms]]
