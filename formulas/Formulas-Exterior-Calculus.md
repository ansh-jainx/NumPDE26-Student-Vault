---
tags: [formulas, chapter-13, FEEC, exterior-calculus]
---

# Exterior Calculus — Quick Reference

---

## Continuous de Rham operators

$$d^\ell: \Lambda^\ell(\Omega) \to \Lambda^{\ell+1}(\Omega), \qquad d^{\ell+1}d^\ell = 0$$

3D vector proxy chain:
$$H^1 \xrightarrow{\nabla} H(\mathrm{curl}) \xrightarrow{\mathrm{curl}} H(\mathrm{div}) \xrightarrow{\mathrm{div}} L^2$$

## Weak Maxwell wave form (schematic)

Find $e(t)\in H_0\Lambda^1$, $b(t)\in H\Lambda^2$:
$$m_1(\partial_t e, w) + c(b,w) = \ell_e(w), \qquad m_2(\partial_t b, z) - c(e,z)=0$$

with bilinear forms induced by material laws and exterior derivative couplings.

## Discrete cochain derivatives

$$\widetilde d^\ell: C^\ell(\mathcal M)\to C^{\ell+1}(\mathcal M), \qquad \widetilde d^{\ell+1}\widetilde d^\ell = 0$$

Matrix form via incidence operators:
$$\mathbf D_{\ell+1}\mathbf D_\ell = 0.$$

## Whitney spaces

$$W^\ell(\mathcal M)=\text{span}\{\beta_f^\ell: f\in \mathcal F^\ell(\mathcal M)\}, \qquad d^\ell W^\ell(\mathcal M)\subset W^{\ell+1}(\mathcal M).$$

## Magnetostatics A-based saddle point

$$
\begin{pmatrix}
\mathbf A & \mathbf B^T \\
\mathbf B & \mathbf 0
\end{pmatrix}
\begin{pmatrix}
\mathbf a\\
\mathbf p
\end{pmatrix}
=
\begin{pmatrix}
\mathbf f\\
\mathbf 0
\end{pmatrix}
$$

LBB conditions (continuous/discrete) ensure stability and uniqueness up to gauge.

---

**Related:** [[Exterior-Derivative-and-de-Rham-Complex]], [[Whitney-Forms]], [[Magnetostatics-Saddle-Point-LBB]], [[Week-11-FEEC-I]], [[Week-12-FEEC-II-and-EM-Waves]], [[Week-13-FEEC-Magnetostatics]]
