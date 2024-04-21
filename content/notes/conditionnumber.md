---
title: Condition Number
date: 2024-04-20
tags:
  - sapling
enableToc: false
---

Gradient converges exponentially fast to a the global minimum with the rate controlled by the *condition number* of the function. 

The condition number $(k_f)$ is the ratio of the largest  eigenvalue of the Hessian matrix($H$) and the smallest eigenvalue of the [[notes/tangentkernel|tangent kernel]] ($K$) of the function.

$$
k_f = \frac{\lambda_{\max} H}{\lambda_{\min} K}
$$

**In an ideal world, we would require the $\lambda_{\min} K$ to be very large and $\lambda_{\max} H$ to be very small. This would mean that the function is very well conditioned and the gradient descent converges very fast.**


If the condition number is large, the function is ill-conditioned and the convergence of gradient descent is slow.



The condition number of a matrix, especially in the context of numerical linear algebra, is a measure of how sensitive the solution of a system of linear equations is to errors in the data or perturbations. It is also used more generally to describe the sensitivity of a function to its inputs. The condition number is influenced by multiple factors:

1. Scale of the Matrix: The scale of the numbers in the matrix can affect the condition number. If the matrix is poorly scaled (i.e., it has very large or very small numbers), it can have a high condition number.
2. Orthogonality of Vectors: If the vectors in the matrix are close to orthogonal, the matrix tends to have a lower condition number. Matrices with vectors that are nearly linearly dependent will have higher condition numbers.
3. Matrix Norm: The condition number is defined in terms of a matrix norm. Changes in the matrix norm (induced by changes in the matrix entries) can lead to changes in the condition number.

To make the condition number smaller and improve numerical stability, one can:

* Rescale the Matrix: Pre-multiplying by a diagonal matrix with appropriate scaling factors can improve the condition number. This is known as equilibration.
* Use Singular Value Decomposition (SVD): SVD can be used to regularize a problem or to compute a more numerically stable solution.
* Regularization Techniques: In problems like linear regression, regularization methods like Ridge Regression or Lasso Regression can improve the condition number by adding a penalty term that discourages large coefficients.
* Increase Precision: Using a higher precision for numerical computations can sometimes mitigate the effects of a high condition number, but it doesn't reduce the condition number itself.
* Perturbation: Small changes to the matrix (perturbation) can sometimes reduce the condition number, but this method needs to be applied carefully as it changes the original problem.
Row or Column Operations: Sometimes, performing certain row or column operations (like in Gaussian elimination) can lead to a matrix with a smaller condition number.
* Preconditioning: Before solving a linear system, applying a preconditioner can transform the system into one that has a better condition number.

It's important to note that there is often a trade-off between improving the condition number and maintaining the accuracy or integrity of the original problem. The appropriate technique depends on the specific context and requirements of the application at hand.