---
tags: [chapter-12, Stokes, pressure, instability, exam-critical]
first_appears: "[[Week-10-Stokes-II]]"
---

# Pressure Instability

**Reference:** §12.3.1

---

## The problem

Naive Galerkin with **equal-order** elements ($P_1$ velocity, $P_1$ pressure) for Stokes:

- The discrete pressure space $Q_h$ contains **spurious modes** (approximate null space of discrete divergence operator)
- Pressure solution oscillates wildly — **not** a physical artifact
- Violates **discrete LBB** (discrete inf-sup constant $\beta_h \to 0$ as $h \to 0$)

> [!warning] Symptom
> Checkerboard pressure patterns, non-convergence of $p_h$ even when $\mathbf{u}_h$ looks reasonable.

## Why it happens

The discrete constraint $b(\mathbf{u}_h, q_h) = 0$ is too weak for $Q_h = P_1$ — many pressure modes satisfy it approximately without controlling gradients.

## Remedies

| Method | Idea |
|--------|------|
| [[Taylor-Hood-FEM]] | $P_2$ velocity, $P_1$ pressure — stable pair |
| [[Crouzeix-Raviart-FEM]] | Non-conforming $P_1$ velocity on edges + $P_0$ pressure |
| Stabilized $P_1$–$P_1$ | Add penalty terms (Problem 12-5) |

---

**Problems:** 12-1, 12-5 | **Related:** [[LBB-Condition]], [[Taylor-Hood-FEM]], [[Crouzeix-Raviart-FEM]]
