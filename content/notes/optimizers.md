---
title: Gradient Descent and optimizers
date: 2024-04-20
tags:
  - sapling
enableToc: false
---


## Gradient Descent

If wee initialize the parameters at some $w_0 \in \mathbb{R}^d$, the gradient descent algorithm updates the parameters as follows:

$$
w_{t+1} = w_t - \eta \nabla L(w_t)
$$

where $ \eta $ is the learning rate and $ \nabla L(w_t) $ is the gradient of the loss function $ L $ at $ w_t $.


It decreases the value of the loss at each iteration, as long as the learning rate is small enough and the value of the gradient is nonzero. Eventually, this should result in gradient descent coming close to a point where the gradient is zero.



We can prove that gradient descent works under the assumption that the second derivative of the objective is bounded. Suppose that for some constant $ \mu > 0 $, for all $ x $ in the space and for any vector $ v $ in $ \mathbb{R}^d $,

$$
|v^T \nabla^2 L(x) v| \leq \mu \|v\|^2.
$$
Here, $ \nabla^2 L(x) $ denotes the matrix of partial derivatives of the loss function $ L $. This is equivalent to the condition that $ \| \nabla^2 L(x) \|_2 \leq \mu $ 

Starting from this condition, let's look at how the objective changes over time as we run gradient descent with a fixed step size. From Taylor's theorem, there exists a $ \xi $ such that

$$
L(w_{t+1}) = L(w_t - \eta \nabla L(w_t)) 
$$
$$
= L(u_t) - \eta (\nabla f(u_t))^T \nabla L(u_t) + \frac{1}{2} \eta^2 (\nabla L(u_t))^T \nabla^2 L(\xi_t) (\nabla L(u_t))
$$
$$
\leq L(u_t) - \eta \|\nabla L(u_t)\|^2 + \frac{\eta^2 L}{2} \|\nabla L(u_t)\|^2 = f(u_t) - \eta ( 1 - \frac{\eta L}{2} ) \|\nabla f(u_t)\|^2.
$$

If we choose our step size $ \eta $ to be small enough that $ 1 > \eta L $, then,

$$
L(u_{t+1}) \leq L(u_t) - \frac{\eta}{2} \|\nabla L(u_t)\|^2
$$
$$
\frac{\eta}{2} \|\nabla L(u_t)\|^2 \leq L(u_t) - L(u_{t+1})
$$

The objective is guaranteed to decrease at each iteration. 

Now, if we sum this up across $ T $ iterations of gradient descent, we get

$$
\frac{\eta}{2 } \sum_{t=0}^{T-1} \|\nabla L(u_t)\|^2 \leq \sum_{t=0}^{T-1} (L(u_t) - L(u_{t+1})) = L(u_0) - f(u_T) \leq L(u_0) - L^*
$$

where $ L^* $ is the global minimum value of the loss function $ L $. From here, we can get

$$
\min_{t \in \{0, ..., T\}} \|\nabla L(u_t)\|^2 \leq \frac{1}{T} \sum_{t=0}^{T-1} \|\nabla L(u_t)\|^2 \leq \frac{2(L(u_0) - L^*)}{\eta T}.
$$

This means that the smallest gradient we observe after $ T $ iterations is getting smaller proportional to $ 1/T $. So gradient descent converges (as long as we look at the smallest observed gradient).

We have a metric to measure the rate of this convergence. It is called the [[notes/conditionnumber| condition number]] ($k_f$) of the function. The condition number is the ratio of the largest eigenvalue of the Hessian matrix to the smallest eigenvalue of the kernel function. If the condition number is large, the function is ill-conditioned and the convergence of gradient descent is slow.

$$
k_f = \frac{\lambda_{\max} H}{\lambda_{\min} K}
$$

If we take the step size($\eta$) to the inverse of the maximum curvature of the hessian matrix. We have an exponential convergence of the gradient descent algorithm.



$$
L(w_t) \leq (1-\frac{1}{k_f})^T L(w_0)
$$

A condition number which is big would mean the loss barely changes each step and a small condition number would mean the loss changes a lot each step.

*Proof of this is pretty complicated, take a look [here](https://www.cs.cornell.edu/courses/cs4787/2020sp/lectures/Lecture2.pdf)*

## Stochastic Gradient Descent (SGD)

## Mini-Batch Gradient Descent

# Adaptive Learning Rates



## AdaGrad

## RMSProp

## Adam

