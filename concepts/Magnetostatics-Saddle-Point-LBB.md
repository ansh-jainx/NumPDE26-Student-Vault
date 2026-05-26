---
tags: [chapter-13, FEEC, magnetostatics, saddle-point, lbb, exam-critical]
first_appears: "[[Week-13-FEEC-Magnetostatics]]"
---

# Magnetostatics Saddle-Point LBB

**Reference:** §13.3.3.3–§13.3.3.4

---

## Mixed formulation

Gauge-constrained vector-potential magnetostatics leads to a saddle-point problem:

$$\begin{pmatrix} A & B^T \\\\ B & 0 \end{pmatrix}\begin{pmatrix} a \\\\ p \end{pmatrix} = \begin{pmatrix} f \\\\ 0 \end{pmatrix}$$

This mirrors Stokes structure from [[Stokes-Saddle-Point]].

## Discrete stability

Whitney spaces satisfy discrete compatibility properties needed for:
- ellipticity on $\ker B$ (LBB1)
- inf-sup condition for $B$ (LBB2)

> [!theorem] Exam-critical
> Discrete LBB is the key guarantee that FEEC magnetostatics does not suffer from spurious gauge modes.

---

**Problems:** 13-2, 13-3 | **Related:** [[LBB-Condition]], [[Magnetostatics-Vector-Potential]], [[Taylor-Hood-FEM]]
