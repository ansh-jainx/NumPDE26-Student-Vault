---
tags: [chapter-3, error-estimate, best-approximation, exam-critical]
first_appears: "[[Week-05-Parametric-FEM-and-Error]]"
---

# Céa's Lemma

**Reference:** §3.1.3 (Thm 3.1.3.7)

> [!info] Naming
> The lecture notes present this as Thm 3.1.3.7. The name "Céa's Lemma" is standard in the wider literature but not used in the notes.

---

## Statement (Thm 3.1.3.7)

If $a(\cdot,\cdot)$ is continuous (constant $C_a$) and coercive (constant $\alpha$) on $V_0$, then for any Galerkin subspace $V_{h,0} \subset V_0$:

$$\|u - u_h\|_a \leq \frac{C_a}{\alpha}\,\inf_{v_h \in V_{h,0}} \|u - v_h\|_a$$

The FEM error is bounded by the **best approximation error** times the ratio $C_a/\alpha$.

## Key Constants

| Constant | From | Role |
|----------|------|------|
| $C_a$ | Continuity of $a$ | $\|a(u,v)\| \leq C_a\|u\|\|v\|$ |
| $\alpha$ | Coercivity of $a$ | $a(v,v) \geq \alpha\|v\|^2$ |
| $C_a/\alpha$ | Quasi-optimality constant | Controls condition number |

## For Symmetric $a$

The factor $C_a/\alpha$ disappears — [[Galerkin-Orthogonality]] gives the exact best approximation property:

$$\|u - u_h\|_a = \inf_{v_h \in V_{h,0}} \|u - v_h\|_a$$

> [!tip] The "interpolation game"
> Céa + interpolation estimates = a priori FEM error bounds. Bound the infimum by choosing $v_h = I_h u$ (the interpolant of $u$): $\inf_{v_h}\|u - v_h\|_a \leq \|u - I_h u\|_a$. See [[Interpolation-Error-Estimates]].

---

**Problems:** 3-15, 3-19, 3-21 | **Related:** [[Galerkin-Orthogonality]], [[Interpolation-Error-Estimates]], [[Lax-Milgram-Theorem]], [[A-Priori-FEM-Error-Estimates]]
