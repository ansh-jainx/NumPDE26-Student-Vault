---
tags: [chapter-13, FEEC, Maxwell, wave-equation]
first_appears: "[[Week-12-FEEC-II-and-EM-Waves]]"
---

# Electromagnetic Wave Equations

**Reference:** §13.3.2.1–§13.3.2.3

---

## FEEC wave model

Combining Maxwell equations with linear material laws gives first-order and second-order evolution formulations for electromagnetic fields.

Semi-discrete FEEC form uses Whitney spaces and yields matrix ODE systems analogous to [[Method-of-Lines]] in Week 7.

## Core structure

- Constraint propagation is built into the variational system.
- Energy balance mirrors wave-equation behavior.
- Timestepping is implicit or structure-preserving due to non-diagonal mass operators for higher-degree forms.

> [!tip] Bridge to Week 7
> EM wave MOL follows the same pattern $M \dot u + Ku = f$, but with $H(\mathrm{curl})$-conforming spaces instead of scalar $H^1$ spaces.

---

**Problems:** 13-4 | **Related:** [[Whitney-Forms]], [[Method-of-Lines]], [[Timestepping-MOL]]
