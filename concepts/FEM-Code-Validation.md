---
tags: [chapter-3, validation, debugging, convergence-testing]
first_appears: "[[Week-06-Convergence-and-Accuracy]]"
---

# FEM Code Validation

**Reference:** §3.8

---

## The Validation Recipe

1. Choose a problem with **known exact solution** (or manufacture one)
2. Solve on a sequence of uniformly refined meshes ($h \to 0$)
3. Compute errors in $H^1$-seminorm and $L^2$-norm
4. Plot errors vs $h$ on **log-log axes**
5. Check that slopes match theoretical predictions from [[A-Priori-FEM-Error-Estimates]]

## Manufactured Solutions

Choose $u$ first, compute $f = -\Delta u$ (or the appropriate PDE operator), use as RHS. This guarantees a known exact solution for any domain.

> [!tip] Smoke test
> If observed convergence rates don't match theory, check in order:
> 1. Assembly (element matrices correct?)
> 2. Boundary conditions (essential BCs properly enforced?)
> 3. Quadrature order (sufficient for the integrands?)
> 4. Regularity of chosen exact solution (smooth enough for optimal rates?)

## Expected Rates

For degree-$p$ FEM on a shape-regular mesh with smooth exact solution on a convex domain:

| Norm | Expected slope |
|------|---------------|
| $\|u - u_h\|_{L^2}$ | $p + 1$ |
| $|u - u_h|_{H^1}$ | $p$ |

If slopes are lower: suspect reduced regularity ([[Elliptic-Regularity]]) or a bug.

---

**Problems:** 3-2 | **Related:** [[A-Priori-FEM-Error-Estimates]], [[Assembly-Algorithm]]
