---
tags: [chapter-13, FEEC, magnetostatics, vector-potential]
first_appears: "[[Week-13-FEEC-Magnetostatics]]"
---

# Magnetostatics Vector Potential

**Reference:** §13.3.3.2

---

## A-based formulation

Set magnetic flux as $b = d^1 a$ (vector proxy: $b = \mathrm{curl}\,a$) with unknown 1-form potential $a$.

Variational spaces are $H(\mathrm{curl})$-type and naturally discretized by Whitney 1-forms.

## Gauge issue

Potential is not unique: $a$ and $a + d^0 \phi$ yield the same $b$.
Gauge constraints or mixed saddle-point formulations are required for uniqueness and stability.

> [!warning] Null-space handling
> Ignoring gauge freedom causes singular systems and unstable numerics.

---

**Problems:** 13-2, 13-3 | **Related:** [[Magnetostatics-Saddle-Point-LBB]], [[Whitney-Forms]], [[LBB-Condition]]
