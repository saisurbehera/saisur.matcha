---
title: Distance Metrics
date: 2024-04-06
---


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