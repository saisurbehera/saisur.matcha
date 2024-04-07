---
title: Wigner’s surmise
date: 2024-04-06
---

# Wigner’s surmise



Consider a 2 x 2 GOE matrix \( H_s = \left( \begin{array}{cc}
x_1 & x_3 \\
x_3 & x_2 \\
\end{array} \right) \) with \( x_1, x_2 \sim \mathcal{N}(0, 1) \) and \( x_3 \sim \mathcal{N}(0, 1/2) \). What is the pdf \( \rho(s) \) of the spacing \( s = \lambda_2 - \lambda_1 \) between its two eigenvalues (\( \lambda_2 > \lambda_1 \))?

The two eigenvalues are random variables, given in terms of the entries by the roots of the characteristic polynomial

$$ \lambda^2 - \text{Tr}(H_s)\lambda + \text{det}(H_s), $$

therefore \( \lambda_{1,2} = (x_1 + x_2 \pm \sqrt{(x_1 - x_2)^2 + 4x_3^2})/2 \) and \( s = \sqrt{(x_1 - x_2)^2 + 4x_3^2} \).

By definition, we have

$$
\rho(s) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} \frac{e^{-\frac{1}{2}x_1^2} e^{-\frac{1}{2}x_2^2} e^{-x_3^2}}{\sqrt{2\pi} \sqrt{2\pi} \sqrt{\pi}} \delta \left( s - \sqrt{(x_1 - x_2)^2 + 4x_3^2} \right) dx_1 dx_2 dx_3.
$$

Changing variables as

$$
\left\{ \begin{array}{l}
x_1 - x_2 = r \cos \theta \\
2x_3 = r \sin \theta \\
x_1 + x_2 = \psi \\
\end{array} \right.
\quad \Rightarrow \quad
\left\{ \begin{array}{l}
x_1 = \frac{r \cos \theta + \psi}{2} \\
x_2 = \frac{\psi - r \cos \theta}{2} \\
x_3 = \frac{r \sin \theta}{2} \\
\end{array} \right.
$$

and computing the corresponding Jacobian

$$
J = \text{det} \left( \begin{array}{ccc}
\frac{\partial x_1}{\partial r} & \frac{\partial x_1}{\partial \theta} & \frac{\partial x_1}{\partial \psi} \\
\frac{\partial x_2}{\partial r} & \frac{\partial x_2}{\partial \theta} & \frac{\partial x_2}{\partial \psi} \\
\frac{\partial x_3}{\partial r} & \frac{\partial x_3}{\partial \theta} & \frac{\partial x_3}{\partial \psi} \\
\end{array} \right)
= \text{det} \left( \begin{array}{ccc}
\cos \frac{\theta}{2} & -\frac{r \sin \frac{\theta}{2}}{2} & \frac{1}{2} \\
-\cos \frac{\theta}{2} & \frac{r \sin \frac{\theta}{2}}{2} & \frac{1}{2} \\
\sin \frac{\theta}{2} & \frac{r \cos \frac{\theta}{2}}{2} & 0 \\
\end{array} \right)
= -\frac{r}{4},
$$

One obtains


$$p(s) = \frac{1}{8\pi^{3/2}} \int_0^\infty dr r \delta(s - r) \int_0^{2\pi} d\theta \int_{-\infty}^\infty d\psi e^{-\frac{1}{2}\left[ \left( \frac{r \cos \theta + \psi}{2} \right)^2 + \left( \frac{\psi - r \cos \theta}{2} \right)^2 + \frac{r^2 \sin^2 \theta}{2} \right]} \\
= \frac{\sqrt{4\pi s}}{8\pi^{3/2}} \int_0^{2\pi} d\theta e^{-\frac{s^2}{2}\left[ \frac{\cos^2 \theta}{2} + \frac{\sin^2 \theta}{2} \right]} 
= \frac{s}{2}e^{-\frac{s^2}{4}}.$$