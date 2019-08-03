---
layout: post
title: "Outlier correction Analysis"
author: "An Ambivert's pen"
headcon: "Removing outliers"
---

```python
import pandas as pd
import numpy as np
import math
```

## Reading the file


```python
fil = pd.read_csv('sleep_cleaned.csv')
print fil.shape
fil.head(5)
```

    (134, 18)





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>time_sleep</th>
      <th>no_of_hrs</th>
      <th>minutes_to_sleep</th>
      <th>wake_up</th>
      <th>day_sleep</th>
      <th>tracker</th>
      <th>use_tv</th>
      <th>sleep_alone</th>
      <th>sep_sleep_place</th>
      <th>comfort</th>
      <th>perf</th>
      <th>trouble_sleep</th>
      <th>trouble_back_to_sleep</th>
      <th>medication</th>
      <th>routine</th>
      <th>rate</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>5</td>
      <td>1</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>1</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>4</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## calculate interquartile range (75 and 25th percentile)


```python
q3,q1=np.percentile(fil['age'], [75,25])
iqr=q3-q1
h_cutoff = iqr*3
low1=q1-h_cutoff
up1=q3+ h_cutoff
print q3,q1
print low1,up1
#print np.mean(fil['age'])
```

    20.0 18.0
    12.0 26.0



```python
ind1 = np.where(fil['age']<low1)
print "ind1",ind1[0]
ind2 = np.where(fil['age']>up1)
print "ind2",ind2[0]
ind = np.concatenate((ind1,ind2),axis=1)
print "ind",ind[0]
```

    ind1 []
    ind2 [111 131]
    ind [111 131]


## drop rows that are outliers


```python
fil=fil.drop(fil.index[ind[0]])
```


```python
print fil.shape
```

    (132, 18)


## replace outliers with 5th and 95th percentile


```python
fil1 = pd.read_csv('sleep_cleaned.csv')
q05,q95 = np.percentile(fil1['age'],[5,95])
q05 = math.ceil(q05)
q95 = math.ceil(q95)
print q05,q95
fil1.loc[ind[0]]
```

    18.0 21.0





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>time_sleep</th>
      <th>no_of_hrs</th>
      <th>minutes_to_sleep</th>
      <th>wake_up</th>
      <th>day_sleep</th>
      <th>tracker</th>
      <th>use_tv</th>
      <th>sleep_alone</th>
      <th>sep_sleep_place</th>
      <th>comfort</th>
      <th>perf</th>
      <th>trouble_sleep</th>
      <th>trouble_back_to_sleep</th>
      <th>medication</th>
      <th>routine</th>
      <th>rate</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>111</th>
      <td>1000</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>5</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>131</th>
      <td>100</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
for i in ind1[0]:
    fil1.at[i,'age']=q05
for i in ind2[0]:
    fil1.at[i,'age']=q95
fil1.loc[ind[0]]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>time_sleep</th>
      <th>no_of_hrs</th>
      <th>minutes_to_sleep</th>
      <th>wake_up</th>
      <th>day_sleep</th>
      <th>tracker</th>
      <th>use_tv</th>
      <th>sleep_alone</th>
      <th>sep_sleep_place</th>
      <th>comfort</th>
      <th>perf</th>
      <th>trouble_sleep</th>
      <th>trouble_back_to_sleep</th>
      <th>medication</th>
      <th>routine</th>
      <th>rate</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>111</th>
      <td>21</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>5</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>131</th>
      <td>21</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## replace outliers with median


```python
fil2 = pd.read_csv('sleep_cleaned.csv')
median_doc =  math.ceil(np.median(fil2['age']))
print np.median(fil2['age'])
for i in ind[0]:
    fil2.at[i,'age'] = median_doc
fil2.loc[ind[0]]
```

    19.0





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>time_sleep</th>
      <th>no_of_hrs</th>
      <th>minutes_to_sleep</th>
      <th>wake_up</th>
      <th>day_sleep</th>
      <th>tracker</th>
      <th>use_tv</th>
      <th>sleep_alone</th>
      <th>sep_sleep_place</th>
      <th>comfort</th>
      <th>perf</th>
      <th>trouble_sleep</th>
      <th>trouble_back_to_sleep</th>
      <th>medication</th>
      <th>routine</th>
      <th>rate</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>111</th>
      <td>19</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>5</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>131</th>
      <td>19</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## replace outliers with mean


```python
fil3 = pd.read_csv('sleep_cleaned.csv')
mean_doc = math.ceil(np.mean(fil3['age']))
print ind[0]
for i in ind[0]:
    print i
    fil3.at[i,'age'] = mean_doc
    
fil3.loc[ind[0]]
```

    [111 131]
    111
    131





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>age</th>
      <th>time_sleep</th>
      <th>no_of_hrs</th>
      <th>minutes_to_sleep</th>
      <th>wake_up</th>
      <th>day_sleep</th>
      <th>tracker</th>
      <th>use_tv</th>
      <th>sleep_alone</th>
      <th>sep_sleep_place</th>
      <th>comfort</th>
      <th>perf</th>
      <th>trouble_sleep</th>
      <th>trouble_back_to_sleep</th>
      <th>medication</th>
      <th>routine</th>
      <th>rate</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>111</th>
      <td>28</td>
      <td>0</td>
      <td>3</td>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>5</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>131</th>
      <td>28</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

