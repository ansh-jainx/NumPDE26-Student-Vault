---
tags: [chapter-1, boundary-conditions, Dirichlet, Neumann, Robin, exam-critical]
first_appears: "[[Week-02-Elliptic-BVPs-II]]"
---

# Boundary Conditions for Elliptic BVPs

**Reference:** §1.7

---

## Types of Boundary Conditions

For $-\operatorname{div}(\kappa\,\nabla u) = f$ in $\Omega$ with boundary $\partial\Omega = \Gamma_D \cup \Gamma_N \cup \Gamma_R$:

| Type | Condition | Physical meaning |
|------|-----------|-----------------|
| **Dirichlet** | $u = g$ on $\Gamma_D$ | Prescribed value (temperature, displacement) |
| **Neumann** | $\kappa\,\nabla u \cdot \mathbf{n} = h$ on $\Gamma_N$ | Prescribed flux (insulation if $h=0$) |
| **Robin** | $\kappa\,\nabla u \cdot \mathbf{n} + c\,u = h$ on $\Gamma_R$ | Convective cooling, impedance |

## Effect on Variational Formulation

After multiplying by test function $v$ and applying [[Essential-vs-Natural-BCs|Green's formula]]:

| BC type | Where it goes | Effect |
|---------|--------------|--------|
| Dirichlet | **Trial/test space** | $u \in V = \{v \in H^1: v|_{\Gamma_D} = g\}$, $v \in V_0 = \{v \in H^1: v|_{\Gamma_D} = 0\}$ |
| Neumann | **Load** $\ell(v)$ | $\ell(v) \mathrel{+}= \int_{\Gamma_N} h\,v\,\mathrm{d}S$ |
| Robin | **Both** $a$ and $\ell$ | $a(u,v) \mathrel{+}= c\int_{\Gamma_R} u\,v\,\mathrm{d}S$, $\ell(v) \mathrel{+}= \int_{\Gamma_R} h\,v\,\mathrm{d}S$ |

> [!warning] Pure Neumann problem
> If $\Gamma_D = \emptyset$ (no Dirichlet BC), then $a(u,v) = \int \nabla u \cdot \nabla v$ is **not coercive** on $H^1$ (constant functions have zero energy). Need compatibility: $\int_\Omega f + \int_{\Gamma_N} h = 0$, and solution is unique only up to a constant.

---

**Problems:** 1-3, 1-6, 1-8, 1-9 | **Related:** [[Essential-vs-Natural-BCs]], [[Essential-BC-Treatment]], [[Method-of-Lines]]
