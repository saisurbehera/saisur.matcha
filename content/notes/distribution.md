---
title: Distributions summarized
date: 2024-04-07
tags:
  - evergreen
enableToc: false
---


# Bernoulli distribution

The Bernoulli distribution is a discrete probability distribution for a random variable which takes the value 1 with probability $p$ and the value 0 with probability $q = 1 - p$. 

$$ f(k;p) = p^k(1-p)^{1-k} \text{ for } k \in \{0,1\} $$

Which is basiically, at k=1 (success) probability is $p$ and at k=0(failure) probability is $1-p$.


### Mean 

The mean of the Bernoulli distribution is $p$. 

Simple proof:
$$ E[X] = \sum_{k=0}^{1} k \cdot f(k;p) = 0 \cdot (1-p) + 1 \cdot (1 \cdot p = p) = p $$

### Variance

The variance of the Bernoulli distribution is $p(1-p)$.

Simple proof:
$$ E[X^2] = \sum_{k=0}^{1} k^2 \cdot f(k;p) = 0^2 \cdot (1-p) + 1^2 \cdot p = p $$

$$ Var[X] = E[X^2] - E[X]^2 = p - p^2 = p(1-p) $$


# Bivariate Gaussian distribution

###### Have to add the formulae and the properties of the bivariate gaussian distribution