---
title: Math terms i have no idea about 
date: 2024-04-14
tags:
  - sapling
enableToc: false
---

In this page, we will be discussing some math terms that are used in machine learning and deep learning that i have no idea about.

## Lipschitz continuity

Given two metric spaces $(X, d_X)$ and $(Y, d_Y)$, a function $f: X \rightarrow Y$ is said to be Lipschitz continuous if there exists a constant $K \geq 0$ such that for all $x_1, x_2 \in X$.

Any such $K$ is called a Lipschitz constant for the function $f$. The smallest constant $K$ for which the inequality holds is called the Lipschitz constant of $f$.

Think of a double cone, where the slope of the cone is the Lipschitz constant. The function is Lipschitz continuous if the slope of the cone is bounded.

## Krylov subspace

Given a matrix $A \in \mathbb{R}^{n \times n}$ and a vector $b \in \mathbb{R}^n$, the Krylov subspace of order $m$ is defined as:

$$ \mathcal{K}_m(A, b) = \text{span}\{b, Ab, A^2b, \ldots, A^{m-1}b\} $$

## Polyak-Lojasiewicz inequality

Polyak-Lojasiewicz inequality is a mathematical inequality that is used to prove the convergence of optimization algorithms. It states that the difference between the function value and the minimum value of the function is bounded by the gradient of the function. 

$$ f(x) - f(x^*) \leq \frac{1}{2\beta} ||\nabla f(x)||^2 $$ 

where $f(x)$ is the function value at $x$, $f(x^*)$ is the minimum value of the function, $\nabla f(x)$ is the gradient of the function at $x$, and $\beta$ is a constant that depends on the function. 

**This can also translate to if the magnitude of the gradient of the loss function is greater than constant times the loss function, we have exponential convergence of gradients.**

We care about a more simpler version of this inequality, the minimum value of the function is hard to guess, so we forget about the $f(x^*)$ term. We first prove this simpler form of the inequality and then we will see how it can be used to prove the convergence of optimization algorithms.
