---
tags: [chapter-13, FEEC, Sobolev, Hcurl, Hdiv]
first_appears: "[[Week-11-FEEC-I]]"
---

# Sobolev Spaces of Forms

**Reference:** §13.1.5

---

## Function spaces for Maxwell

FEEC reformulates regularity using spaces compatible with $d^\ell$:

- $H\Lambda^0 \sim H^1$
- $H\Lambda^1 \sim H(\mathrm{curl})$
- $H\Lambda^2 \sim H(\mathrm{div})$

These spaces encode tangential/normal trace behavior needed by electromagnetic boundary conditions.

## Variational implication

Use trial and test spaces where derivatives exist weakly:

$$u \in H\Lambda^\ell,\quad d^\ell u \in L^2\Lambda^{\ell+1}$$

> [!warning] Wrong space = unstable method
> Using $H^1$-conforming spaces where $H(\mathrm{curl})$ conformity is needed breaks structure and can violate physical constraints.

---

**Problems:** 13-2, 13-4 | **Related:** [[Exterior-Derivative-and-de-Rham-Complex]], [[Whitney-Forms]], [[Electromagnetic-Wave-Equations]]
