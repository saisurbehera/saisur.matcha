---
title:  Part 1 Layer
date: 2023-10-06
tags:
  - seed
enableToc: false
---

## Layer code

Basically represent the equation: $Wx+b$ where $W$ is the weight matrix and $b$ is the bias. 

```
class Layer:
    
    def __init__(M,N):
        self.weight = self.random.random((M,N))
        self.bias = np.zeros(M)
    
    def __forward(x):
        return np.inner(W,x) + self.bias
        
```

So the weight inialization is done by the zeros function and the forward pass is done by the inner product of the weight and the input plus the bias. The problem is the weight initialization is from the standard normal. 

This is a problem because:
* Vanishing Gradient Problem
    * If the weights are too small the gradient goes to zero and there is no learning
* Exploding Gradient Problem
    * If the weights are too large the gradient explodes and the outputs make no sense

### Detailed understanding of the problem 



If we initalize the weights from a standard normal distribution. We can see that the values across layers basically go to zero as we go deeper. 

<p align="center" width="100%">
<img width="65%" src="assets/imgtransformers/image.png">
</p>

#### Mathematical proof of problem:
$$
f'(s_k) \approx 1,
$$

$$
\mathrm{Var}[z^{i}] = \mathrm{Var}[x] \prod_{i'=0}^{i-1} \mathrm{Var}[W'^{i'}],
$$

We write $\mathrm{Var}[W'^{i'}]$ for the shared scalar variance of all weights at layer $i'$. Then for a network with $d$ layers,

$$
\mathrm{Var}\left[\frac{\partial \text{Cost}}{\partial s^i}\right] = \mathrm{Var}\left[\frac{\partial \text{Cost}}{\partial s^d}\right] \prod_{i'=i}^{d} n_{i'+1} \mathrm{Var}[W'^{i'}],
$$

$$
\mathrm{Var}\left[\frac{\partial \text{Cost}}{\partial w^i}\right] = \prod_{i'=0}^{i-1} n_{i'} \mathrm{Var}[W'^{i'}] \prod_{i'=i}^{d-1} n_{i'+1} \mathrm{Var}[W'^{i'}] \times \mathrm{Var}[x] \mathrm{Var}\left[\frac{\partial \text{Cost}}{\partial s^d}\right]
$$


As you see the problem, each layers variance is being multiplied. This is the reason, if we see the graph flattens out as the variance increases all the time. 

To fix this, we set the variance of the gradients to be same across layers.

From a forward-propagation point of view, to keep information flowing we would like that

$$
\forall (i, i'), \mathrm{Var}[z^{i}] = \mathrm{Var}[z^{i'}].
$$

From a back-propagation point of view we would similarly like to have

$$
\forall (i, i'), \mathrm{Var}\left[\frac{\partial \text{Cost}}{\partial s^i}\right] = \mathrm{Var}\left[\frac{\partial \text{Cost}}{\partial s^{i'}}\right].
$$


# Kaiming initialization 

In popular terms, we use kaiming and xavier initialization. Kaiming paper takes into account the activation function, whereas Xavier initialization does not. The explanation is described [here](https://pouannes.github.io/blog/initialization/)

Summary:

* Let us assume that, w is symetric across 0 and bias is zero.
* ReLU only cares about the positive part
* So, we care only half of the distribution cause it is symetric therefore we can calculate  $E(x_l^2) = \frac{1}{2} \mathrm{Var(y_{l-1})}  $
* We also know that $\mathrm{Var(y_l) } = n_l\mathrm{Var(w_l x_i) } = n_l (E[w_l^2]E[x_l^2]-E[w_l]^2 E[x_l]^2)$ , we set the weights to be 0 mean so the right side is useless. We also know that $E(w_l^2) = \mathrm{Var(w_l)} $ as mean is zero. Final equation is $n_l \mathrm{Var(w_l)}E[x_l^2]$
* Lets combine previous two points, we get $\mathrm{Var(y_l)} = n_l \mathrm{Var(w_l)} \frac{1}{2} \mathrm{Var(y_{l-1})}$
* For these to not scale up or down, we need $\mathrm{Var(y_l)} = \mathrm{Var(y_{l-1})}$
* Therefore, we need $\mathrm{Var(w_l)} = \frac{2}{n_l}$

### Kaiming Normalization is setting the variance to be $\frac{2}{n_l}$

# Modified Code for layer

```
class Layer:
    
    def __init__(self,M,N, bias = None):
        self.weight = self.kaiming_init(M,N)
        self.bias = bias if bias is not None else np.zeros(M)
    
    def __forward(self,x):
        output = np.inner(self.weight,x)
        if sefl.bias is not None:
            return  output + self.bias
        return temp
    
    def __kaiming_init(self,M,N):
        std_dev = np.sqrt(2.0 / M)
        return np.random.normal(0, std_dev, size=(input_dim, output_dim))
     
```
#### References:

* [Understanding the difficulty of training deep feedforward neural networks](http://proceedings.mlr.press/v9/glorot10a/glorot10a.pdf)
* Pierre Ouannes - [Initialization](https://pouannes.github.io/blog/initialization/)
* [Kaiming He et al. - Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification](https://arxiv.org/abs/1502.01852)