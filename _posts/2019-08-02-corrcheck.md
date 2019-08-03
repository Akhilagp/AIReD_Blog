---
layout: post
title: "Correlation Check"
author: "An Ambivert's pen"
headcon: "Checking correlation"
---

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import time
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB, BernoulliNB, MultinomialNB
import seaborn as sns
from scipy.stats import anderson
```


```python
fil = pd.read_csv('fil1.csv')
fil['trouble_sleep'].corr(fil['trouble_back_to_sleep'])
```




    0.5042803893076943


## Correlation check

```python
corr = fil.corr()
fig = plt.figure()
ax = fig.add_subplot(111)
cax = ax.matshow(corr,cmap='coolwarm', vmin=-1, vmax=1)
fig.colorbar(cax)
ticks = np.arange(0,len(fil.columns),1)
ax.set_xticks(ticks)
plt.xticks(rotation=90)
ax.set_yticks(ticks)
ax.set_xticklabels(fil.columns)
ax.set_yticklabels(fil.columns)
plt.show()
```


![png]({{site.url}}/assets/output_corr_check.png)

