---
title: Tangent Kernels 
date: 2024-04-19
tags:
  - sapling
enableToc: false
---

A tangent kernel for a function $F(w)=y$, where $w \in \mathbb{R}^m$ and $y \in \mathbb{R}^n$. A tanget kernel is a matrix $K \in \mathbb{R}^{n \times n}$ is:

$$
K(w)  = \nabla F(w) \cdot \nabla F(w)^T
$$

Essential, it is gradient of the function $F$ at $w$ multiplied with its transpose.

One important conclusion is if we can get the minimum eigen-value of the tangent kernel is greater than $\mu$, then we satisfy the $\mu$-strong [[notes/mathterms#Polyak-Lojasiewicz inequality|Polyak-Lojasiewicz inequality]]

## Proof:

Let us assume $\lambda_{\min}(K(w)) \geq \mu_M$ on $B$


$$
L(w) = \frac{1}{2} ||F(w) - y||^2
$$

Let us assume that our loss function $L(w)$ expressed as the squared norm of the difference between a function $F(w)$ and some target $y$. 

Let us consider the gradient of the loss function( derivative of the loss function with respect to the weights)

$$
\frac{1}{2} ||\nabla L(w) ||^2 = \frac{1}{2} ||(F(w) - y)^\mathrm{T} \nabla F(w) ||^2 = \frac{1}{2} (F(w) - y)^\mathrm{T} {\color{blue} \nabla F(w) \nabla F(w)^\mathrm{T}} (F(w) - y)
$$

We know that:

$$ K = \nabla F(w) \nabla F(w)^\mathrm{T} $$

So, we can rewrite the above equation as:

$$
\frac{1}{2} ||\nabla L(w) ||^2 = \frac{1}{2} (F(w) - y)^\mathrm{T} K (F(w) - y) = K \cdot \frac{1}{2} || (F(w) - y) ||^2 = K \cdot L(w)
$$

Therefore the gradiant of the loss function is the tangent kernel multiplied by the loss function. 

If we use the initial conditions, we can rewrite the above equation as:

$$
\frac{1}{2} ||\nabla L(w) ||^2 \geq \lambda_{\min}(K(w))  \cdot L(w)
$$

If we see the kernel function, the smallest eigenvalue of the kernel function is $\lambda_{\min}(K)$. If $\lambda_{\min}(K) \geq \mu_M$, then we have the $\mu_M$-strong Polyak-Lojasiewicz inequality. This translates to high convergence of the optimization algorithm.


This is a very important result as it shows that the minimum eigenvalue of the tangent kernel is a key factor in the convergence of the optimization algorithm. If the minimum eigenvalue of the tangent kernel is greater than a certain threshold, then the optimization algorithm will converge exponentially fast. This is a very useful result in practice, as it allows us to analyze the convergence properties of optimization algorithms and design algorithms that converge faster.   

Now a natural question is how we measure the convergence. Read more about in [[notes/conditionnumber| condition number]]