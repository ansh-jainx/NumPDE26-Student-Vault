---
tags: [chapter-9, parabolic, variational-formulation, exam-critical]
first_appears: "[[Week-07-Parabolic-IBVPs]]"
---

# Spatial Variational Formulation (Parabolic)

**Reference:** §9.2.2

---

## Recipe

1. Test PDE with $v \in V_0$ (spatial test functions — no time dependence)
2. Integrate over $\Omega$
3. Integration by parts in space (Green's formula)
4. Apply BCs to boundary terms

> [!tip] Test space rule
> Dirichlet BCs → $V_0 = H_0^1(\Omega)$. Neumann/Robin BCs → $V_0 = H^1(\Omega)$ and boundary integrals survive.

## Abstract Form (§9.2.2.8)

$$m(\dot{u}(t), v) + a(u(t), v) = \ell(t)(v) \quad \forall v \in V_0, \qquad u(0) = u_0$$

- $m(u,v) = \int_\Omega \rho\,u\,v\,\mathrm{d}\mathbf{x}$ — mass (s.p.d.)
- $a(u,v) = \int_\Omega \kappa\,\nabla u \cdot \nabla v\,\mathrm{d}\mathbf{x}$ — stiffness (s.p.d.)
- Since $m$ is time-independent: $m(\dot{u},v) = \frac{d}{dt}m(u,v)$

For non-homogeneous Dirichlet: reduce to $g = 0$ via **offset function trick** (§2.7.6).

---

**Problems:** 9-1(a), 9-2(a), 9-20(a) | **Feeds into:** [[Method-of-Lines]]
