---
tags: [chapter-13, FEEC, discrete-operator, incidence-matrix]
first_appears: "[[Week-12-FEEC-II-and-EM-Waves]]"
---

# Discrete Exterior Derivative

**Reference:** §13.2.1.2

---

## Definition

The discrete derivative $\tilde d^\ell: C^\ell(\mathcal{M}) \to C^{\ell+1}(\mathcal{M})$ is represented by oriented incidence matrices.

It mirrors Stokes' theorem:
$$\tilde d^\ell \,\text{(cochain)} \leftrightarrow \text{boundary sum on } (\ell+1)\text{-facets}.$$

## Algebraic structure

Like the continuous case:
$$\tilde d^{\ell+1}\tilde d^\ell = 0.$$

This guarantees compatibility constraints and eliminates nonphysical source terms at the discrete level.

> [!theorem] Commuting principle
> Cochain derivatives and Whitney interpolation commute in the FEEC pipeline.

---

**Problems:** 13-1, 13-4 | **Related:** [[Cochain-Calculus]], [[Exterior-Derivative-and-de-Rham-Complex]], [[Whitney-Forms]]
