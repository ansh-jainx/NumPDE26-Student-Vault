---
tags: [chapter-13, FEEC, Whitney, finite-elements, exam-critical]
first_appears: "[[Week-12-FEEC-II-and-EM-Waves]]"
---

# Whitney Forms

**Reference:** §13.2.2

---

## Role in FEEC

Whitney forms are finite element shape functions for differential forms. Degree matches geometric entity:

- Whitney 0-forms: nodal (equals $S_1^0$)
- Whitney 1-forms: edge-based ($H(\mathrm{curl})$-conforming)
- Whitney 2-forms: face-based ($H(\mathrm{div})$-conforming)

## Key properties

- Local support on neighboring cells.
- Commuting interpolation with exterior derivative.
- Natural conformity for Maxwell and magnetostatics.

> [!warning] Exam-critical
> Know why Whitney spaces preserve de Rham structure and why this prevents spurious electromagnetic modes.

---

**Problems:** 13-2, 13-4 | **Related:** [[Cochain-Calculus]], [[Discrete-Exterior-Derivative]], [[Sobolev-Spaces-of-Forms]]
