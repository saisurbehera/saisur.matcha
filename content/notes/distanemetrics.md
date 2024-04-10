---
title: Distance Metrics
date: 2024-04-06
---

## Hellinger Distance

The Hellinger distance is a measure of the similarity between two probability distributions. It is defined as:

$$ H^2(P,Q) = \frac{1}{2} \sum_{i=1}^{n} (\sqrt{p_i} - \sqrt{q_i})^2 $$

where $P$ and $Q$ are two probability distributions over the same set of $n$ events.

In the continuous case, the Hellinger distance between two probability density functions $p(x)$ and $q(x)$ is defined as:
$$ H^2(p,q) = \frac{1}{2} \int (\sqrt{p(x)} - \sqrt{q(x)})^2 dx = 1 - \int \sqrt{p(x)q(x)} dx $$    

## Mahalanobis Distance

```
import numpy as np 
import pandas as pd  
import scipy as stats 
  
# calculateMahalanobis function to calculate 
# the Mahalanobis distance 
def calculateMahalanobis(y=None, data=None, cov=None): 
  
    y_mu = y - np.mean(data) 
    if not cov: 
        cov = np.cov(data.values.T) 
    inv_covmat = np.linalg.inv(cov) 
    left = np.dot(y_mu, inv_covmat) 
    mahal = np.dot(left, y_mu.T) 
    return mahal.diagonal() 
```