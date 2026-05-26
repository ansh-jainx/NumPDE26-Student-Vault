---
tags: [exam, exam-critical, chapter-3, deep-dive]
---

# Exam Deep Dive — Convergence Plots

**Theme:** Identifying convergence orders from data (4×) | **Type F** | **HW:** 3-15, 3-19

> Master bank: [[Exam-Master-Bank#Ch3]] | Weeks: [[Week-05-Parametric-FEM-and-Error]], [[Week-06-Convergence-and-Accuracy]]

---

## Anchor exams

| Year | Exam | Problem | Title | HW |
|------|------|---------|-------|-----|
| 2023 | Endterm | 0-1 | Identifying convergence rates from plots | 3-15, 3-19 |
| 2021 | Midterm | 0-2 | Asymptotic convergence of FE and interpolation errors | 3-15 |

PDFs: `NPDE23_Endterm_sols.pdf`, `NPDE21_Midterm_sols.pdf`.

---

## Universal strategy (Type F)

> [!example] HOW TO: Convergence rate from log-log data
> 1. Plot $\log(e_h)$ vs $\log(h)$ where $e_h = \|u - u_h\|$ or energy error.
> 2. Asymptotic slope $p \approx \Delta\log e / \Delta\log h$.
> 3. Compare to expected: $O(h^p)$ in $H^1$ for $P_p$ elements (Céa + interpolation **3.3.2.21**).
> 4. Separate curves: discretization error vs interpolation error $u - I_h u$.
> 5. Flag pre-asymptotic regime (coarse meshes) or pollution (wrong slope / upturn).

---

## 2023 Endterm 0-1

**Focus:** Read multiple curves; match label to FE degree / norm; explain deviation.

**Sections:** §3.1–§3.3, Meta-Thm **9.2.8.5** link for full-discrete analog.

**HW drill:** [[FEM-Error-Analysis-Problems#Problem 3-15]], 3-19.

---

## 2021 Midterm 0-2

**Focus:** Interpolation vs Galerkin error parallel to $O(h^p)$ lines; Galerkin orthogonality argument sketch.

**Theory anchor:** Céa's lemma **3.1.3.7** + best approximation.

---

## Common mistakes

- Reporting slope from non-asymptotic first two points.
- Confusing $L^2$ and $H^1$ convergence orders ($p$ vs $p$ or $p+1$ depending on setting).
- Ignoring logarithmic scale when exam gives semilog axes.

---

## Links

- [[Exam-Problem-Types-Full-Course#Type F — Convergence from data]]
- [[Cea-Lemma]], [[Interpolation-Error-Estimates]], [[FEM-Code-Validation]]
- [[FEM-Error-Analysis-Problems]]
