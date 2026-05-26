---
tags: [chapter-13, FEEC, forms]
first_appears: "[[Week-11-FEEC-I]]"
---

# Differential Forms

**Reference:** §13.1.1–§13.1.3

---

## Core idea

Differential forms unify scalar fields, vector proxies, and integration objects. In FEEC, an $\ell$-form is the natural object integrated over $\ell$-dimensional facets.

| Degree | Typical proxy in 3D | Integrated over |
|---|---|---|
| 0-form | scalar potential | points |
| 1-form | electric field proxy | curves |
| 2-form | magnetic flux proxy | surfaces |
| 3-form | charge density | volumes |

## Why this matters

Maxwell equations are compactly written with forms and the exterior derivative. This makes topology and conservation structure explicit before discretization.

> [!info] FEEC viewpoint
> Choose finite element spaces by form degree, not by ad-hoc vector components.

---

**Problems:** 13-1 | **Related:** [[Exterior-Derivative-and-de-Rham-Complex]], [[Sobolev-Spaces-of-Forms]], [[Whitney-Forms]]
