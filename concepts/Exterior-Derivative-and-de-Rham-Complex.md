---
tags: [chapter-13, FEEC, exterior-derivative, de-rham]
first_appears: "[[Week-11-FEEC-I]]"
---

# Exterior Derivative and de Rham Complex

**Reference:** §13.1.4.2, §13.1.4.3

---

## Exterior derivative

The operators $d^\ell$ map $\ell$-forms to $(\ell+1)$-forms and satisfy $d^{\ell+1} d^\ell = 0$.

In 3D vector proxies:
- $d^0$ corresponds to $\nabla$
- $d^1$ corresponds to $\mathrm{curl}$
- $d^2$ corresponds to $\mathrm{div}$

## de Rham sequence

$$H^1 \xrightarrow{d^0} H(\mathrm{curl}) \xrightarrow{d^1} H(\mathrm{div}) \xrightarrow{d^2} L^2$$

Exactness links kernels and images, giving potential formulations and compatibility constraints.

> [!theorem] Structural identity
> $d^{\ell+1} d^\ell = 0$ is the abstract source of identities such as $\mathrm{curl}\,\nabla = 0$ and $\mathrm{div}\,\mathrm{curl}=0$.

---

**Problems:** 13-2, 13-3 | **Related:** [[Differential-Forms]], [[Sobolev-Spaces-of-Forms]], [[Cochain-Calculus]]
