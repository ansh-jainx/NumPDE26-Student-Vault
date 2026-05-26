---
tags: [chapter-3, variational-crimes, Strang, quadrature, boundary-approximation]
first_appears: "[[Week-06-Convergence-and-Accuracy]]"
---

# Variational Crimes

**Reference:** §3.5

---

## Idea

When the discrete bilinear form $a_h$ differs from the continuous form $a$ (due to quadrature, curved boundary approximation, etc.), the standard Galerkin framework is "violated" — a **variational crime**. [[Cea-Lemma]] no longer applies directly.

## Strang's Second Lemma (§3.5)

Modified error bound with three terms:

$$\|u - u_h\| \leq C\!\left(\inf_{v_h \in V_h}\|u - v_h\| \;+\; \sup_{w_h}\frac{|a(v_h, w_h) - a_h(v_h, w_h)|}{\|w_h\|} \;+\; \|\ell - \ell_h\|\right)$$

| Term | Meaning |
|------|---------|
| $\inf\|u - v_h\|$ | Best approximation (same as Céa) |
| $\|a - a_h\|$ consistency | Error from replacing $a$ by $a_h$ |
| $\|\ell - \ell_h\|$ consistency | Error from replacing $\ell$ by $\ell_h$ |

> [!tip] Exam interpretation
> Strang's Lemma generalizes Céa's Lemma. If there are no crimes ($a_h = a$, $\ell_h = \ell$), it reduces to Céa.

## §3.5.1 — Quadrature Impact

Using numerical quadrature instead of exact integrals changes $a$ to $a_h$. The consistency error is controlled if the quadrature rule is sufficiently accurate for the integrands involved.

## §3.5.2 — Boundary Approximation

Polygonal approximation of a curved domain $\Omega$ means computing on $\Omega_h \neq \Omega$. This introduces geometry error in both $a$ and $\ell$.

> [!warning] Both crimes in parametric FEM
> [[Parametric-FEM|Isoparametric elements]] commit both crimes: the non-affine map requires quadrature (crime 1), and the polynomial boundary is only an approximation (crime 2). See §2.8.4.

---

**Problems:** 3-10 | **Related:** [[Parametric-FEM]], [[Cea-Lemma]], [[Local-Computations]]
