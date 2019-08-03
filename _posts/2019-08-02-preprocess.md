---
layout: post
title: "Data Cleaning and Preprocessing"
author: "An Ambivert's pen"
headcon: "Handling categorical and missing data"
---

```python
import pandas as pd
import numpy as np
```


```python
fil = pd.read_csv('sleep.csv')
fil.shape
```




    (134, 20)




```python
fil.head(5)
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
      <th>Timestamp</th>
      <th>Can we know your name please?</th>
      <th>Your age</th>
      <th>What is your typical time to go to sleep?</th>
      <th>Average number of hours of sleep per night</th>
      <th>How long does it take you to fall asleep after being in bed (Scaled in minutes)?</th>
      <th>How many times ﻿do you wake up in between sleep?</th>
      <th>Do you uncontrollably feel sleepy during the day/ class hours?</th>
      <th>Do you use any fitness / sleep tracking device?</th>
      <th>Sleep Environment [Do you watch TV/ use Mobile phones prior to sleep?]</th>
      <th>Sleep Environment [Do you sleep alone?]</th>
      <th>Sleep Environment [Is your study and sleep space separate?]</th>
      <th>How comfortable is your sleep area?</th>
      <th>Does your sleeping habits affect your mood / academic performance / performance at work ?</th>
      <th>Insomnia [Do you have trouble falling sleep?]</th>
      <th>Insomnia [Do you have trouble returning to sleep after being awaken during the night?]</th>
      <th>Insomnia [Do you use medications to help you sleep?]</th>
      <th>Is your sleep routine consistent ?</th>
      <th>How would you rate your sleep?</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019/02/02 5:14:51 PM GMT+5:30</td>
      <td>NaN</td>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Sometimes</td>
      <td>3</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>No</td>
      <td>No</td>
      <td>Only on weekdays</td>
      <td>3</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019/02/02 5:24:09 PM GMT+5:30</td>
      <td>_AP_The_Don</td>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Never</td>
      <td>2</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>4</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019/02/02 5:32:44 PM GMT+5:30</td>
      <td>Riyaz</td>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>5</td>
      <td>Never</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>4</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019/02/02 5:33:13 PM GMT+5:30</td>
      <td>NaN</td>
      <td>20</td>
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Yes</td>
      <td>Sometimes</td>
      <td>5</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Only on weekdays</td>
      <td>4</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019/02/02 5:34:00 PM GMT+5:30</td>
      <td>Hussain Imthiaz Hussain</td>
      <td>17</td>
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Never</td>
      <td>4</td>
      <td>Always</td>
      <td>Seldom</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>Yes</td>
      <td>4</td>
      <td>Male</td>
    </tr>
  </tbody>
</table>
</div>




```python
drop_cols = fil.columns.values[0:2]
fil=fil.drop(columns=drop_cols)
fil.shape
```




    (134, 18)




```python
print fil.columns.values
```

    ['Your age' 'What is your typical time to go to sleep?'
     'Average number of hours of sleep per night'
     'How long does it take you to fall asleep after being in bed (Scaled in minutes)?'
     'How many times \xef\xbb\xbfdo you wake up in between sleep?'
     'Do you uncontrollably feel sleepy during the day/ class hours?'
     'Do you use any fitness / sleep tracking device?'
     'Sleep Environment [Do you watch TV/ use Mobile phones prior to sleep?]'
     'Sleep Environment [Do you sleep alone?]'
     'Sleep Environment [Is your study and sleep space separate?]'
     'How comfortable is your sleep area?'
     'Does your sleeping habits affect your mood / academic performance / performance at work ?'
     'Insomnia [Do you have trouble falling sleep?]'
     'Insomnia [Do you have trouble returning to sleep after being awaken during the night?]'
     'Insomnia [Do you use medications to help you sleep?]'
     'Is your sleep routine consistent ?' 'How would you rate your sleep?'
     'Gender']



```python
fil.columns = ['age','time_sleep','no_of_hrs','minutes_to_sleep','wake_up','day_sleep','tracker','use_tv','sleep_alone','sep_sleep_place','comfort','perf','trouble_sleep','trouble_back_to_sleep','medication','routine','rate','gender']
```


```python
fil.columns.values
fil.shape
```




    (134, 18)




```python
fil.columns.values
```




    array(['age', 'time_sleep', 'no_of_hrs', 'minutes_to_sleep', 'wake_up',
           'day_sleep', 'tracker', 'use_tv', 'sleep_alone', 'sep_sleep_place',
           'comfort', 'perf', 'trouble_sleep', 'trouble_back_to_sleep',
           'medication', 'routine', 'rate', 'gender'], dtype=object)




```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Sometimes</td>
      <td>3</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>No</td>
      <td>No</td>
      <td>Only on weekdays</td>
      <td>3</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Never</td>
      <td>2</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>4</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>5</td>
      <td>Never</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>4</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20</td>
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Yes</td>
      <td>Sometimes</td>
      <td>5</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Only on weekdays</td>
      <td>4</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Never</td>
      <td>4</td>
      <td>Always</td>
      <td>Seldom</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>Yes</td>
      <td>4</td>
      <td>Male</td>
    </tr>
  </tbody>
</table>
</div>




```python
fil['gender'].fillna('Untold',inplace=True)
```


```python
fil['gender']=np.where(fil['gender']=='Male',0,fil['gender'])
fil['gender']=np.where(fil['gender']=='Female',1,fil['gender'])
fil['gender']=np.where(fil['gender']=='Untold',2,fil['gender'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Sometimes</td>
      <td>3</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>No</td>
      <td>No</td>
      <td>Only on weekdays</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Never</td>
      <td>2</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>5</td>
      <td>Never</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20</td>
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Yes</td>
      <td>Sometimes</td>
      <td>5</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Only on weekdays</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Never</td>
      <td>4</td>
      <td>Always</td>
      <td>Seldom</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>Yes</td>
      <td>4</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
fil['routine']=np.where(fil['routine']=='Yes',0,fil['routine'])
fil['routine']=np.where(fil['routine']=='Only on weekdays',1,fil['routine'])
fil['routine']=np.where(fil['routine']=='No',2,fil['routine'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Sometimes</td>
      <td>3</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>No</td>
      <td>No</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Never</td>
      <td>2</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>2</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>5</td>
      <td>Never</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20</td>
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Yes</td>
      <td>Sometimes</td>
      <td>5</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>1</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Never</td>
      <td>4</td>
      <td>Always</td>
      <td>Seldom</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
fil['medication']=np.where(fil['medication']=='Yes',0,fil['medication'])
fil['medication']=np.where(fil['medication']=='Sometimes',1,fil['medication'])
fil['medication']=np.where(fil['medication']=='Seldom',2,fil['medication'])
fil['medication']=np.where(fil['medication']=='No',3,fil['medication'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Sometimes</td>
      <td>3</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>No</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Never</td>
      <td>2</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>3</td>
      <td>2</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>5</td>
      <td>Never</td>
      <td>No</td>
      <td>No</td>
      <td>3</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20</td>
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Yes</td>
      <td>Sometimes</td>
      <td>5</td>
      <td>Usually</td>
      <td>No</td>
      <td>No</td>
      <td>3</td>
      <td>1</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Never</td>
      <td>4</td>
      <td>Always</td>
      <td>Seldom</td>
      <td>Sometimes</td>
      <td>2</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
fil.dtypes
```




    age                       int64
    time_sleep               object
    no_of_hrs                object
    minutes_to_sleep         object
    wake_up                  object
    day_sleep                object
    tracker                  object
    use_tv                   object
    sleep_alone              object
    sep_sleep_place          object
    comfort                   int64
    perf                     object
    trouble_sleep            object
    trouble_back_to_sleep    object
    medication               object
    routine                  object
    rate                      int64
    gender                   object
    dtype: object




```python
fil['trouble_back_to_sleep']=np.where(fil['trouble_back_to_sleep']=='Yes',0,fil['trouble_back_to_sleep'])
fil['trouble_back_to_sleep']=np.where(fil['trouble_back_to_sleep']=='Sometimes',1,fil['trouble_back_to_sleep'])
fil['trouble_back_to_sleep']=np.where(fil['trouble_back_to_sleep']=='Seldom',2,fil['trouble_back_to_sleep'])
fil['trouble_back_to_sleep']=np.where(fil['trouble_back_to_sleep']=='No',3,fil['trouble_back_to_sleep'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Sometimes</td>
      <td>3</td>
      <td>Sometimes</td>
      <td>Seldom</td>
      <td>3</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Never</td>
      <td>2</td>
      <td>Usually</td>
      <td>No</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>5</td>
      <td>Never</td>
      <td>No</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20</td>
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Yes</td>
      <td>Sometimes</td>
      <td>5</td>
      <td>Usually</td>
      <td>No</td>
      <td>3</td>
      <td>3</td>
      <td>1</td>
      <td>4</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17</td>
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Never</td>
      <td>4</td>
      <td>Always</td>
      <td>Seldom</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
fil['trouble_sleep']=np.where(fil['trouble_sleep']=='Yes',0,fil['trouble_sleep'])
fil['trouble_sleep']=np.where(fil['trouble_sleep']=='Sometimes',1,fil['trouble_sleep'])
fil['trouble_sleep']=np.where(fil['trouble_sleep']=='Seldom',2,fil['trouble_sleep'])
fil['trouble_sleep']=np.where(fil['trouble_sleep']=='No',3,fil['trouble_sleep'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Sometimes</td>
      <td>3</td>
      <td>Sometimes</td>
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
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Never</td>
      <td>2</td>
      <td>Usually</td>
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
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>5</td>
      <td>Never</td>
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
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Yes</td>
      <td>Sometimes</td>
      <td>5</td>
      <td>Usually</td>
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
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Never</td>
      <td>4</td>
      <td>Always</td>
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




```python
fil['perf']=np.where(fil['perf']=='Always',0,fil['perf'])
fil['perf']=np.where(fil['perf']=='Usually',1,fil['perf'])
fil['perf']=np.where(fil['perf']=='Sometimes',2,fil['perf'])
fil['perf']=np.where(fil['perf']=='Never',3,fil['perf'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Sometimes</td>
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
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Never</td>
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
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
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
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Yes</td>
      <td>Sometimes</td>
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
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
      <td>Never</td>
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




```python
fil['sep_sleep_place']=np.where(fil['sep_sleep_place']=='Yes',0,fil['sep_sleep_place'])
fil['sep_sleep_place']=np.where(fil['sep_sleep_place']=='Sometimes',1,fil['sep_sleep_place'])
fil['sep_sleep_place']=np.where(fil['sep_sleep_place']=='Never',2,fil['sep_sleep_place'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
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
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
      <td>Yes</td>
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
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
      <td>Yes</td>
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
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Yes</td>
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
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
      <td>Never</td>
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




```python
fil['sleep_alone']=np.where(fil['sleep_alone']=='Yes',0,fil['sleep_alone'])
fil['sleep_alone']=np.where(fil['sleep_alone']=='Sometimes',1,fil['sleep_alone'])
fil['sleep_alone']=np.where(fil['sleep_alone']=='Never',2,fil['sleep_alone'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
      <td>Sometimes</td>
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
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
      <td>Yes</td>
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
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
      <td>Yes</td>
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
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
      <td>Sometimes</td>
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
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
      <td>Sometimes</td>
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




```python
fil['use_tv']=np.where(fil['use_tv']=='Yes',0,fil['use_tv'])
fil['use_tv']=np.where(fil['use_tv']=='Sometimes',1,fil['use_tv'])
fil['use_tv']=np.where(fil['use_tv']=='Never',2,fil['use_tv'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
      <td>No</td>
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
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>Yes</td>
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
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
      <td>No</td>
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
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
      <td>No</td>
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
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
      <td>No</td>
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




```python
fil['tracker']=np.where(fil['tracker']=='Yes',0,fil['tracker'])
fil['tracker']=np.where(fil['tracker']=='No',1,fil['tracker'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
      <td>Usually</td>
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
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
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
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Always</td>
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
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Sometimes</td>
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
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
      <td>Rarely</td>
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




```python
fil['day_sleep']=np.where(fil['day_sleep']=='Always',0,fil['day_sleep'])
fil['day_sleep']=np.where(fil['day_sleep']=='Usually',1,fil['day_sleep'])
fil['day_sleep']=np.where(fil['day_sleep']=='Sometimes',2,fil['day_sleep'])
fil['day_sleep']=np.where(fil['day_sleep']=='Rarely',3,fil['day_sleep'])
fil['day_sleep']=np.where(fil['day_sleep']=='Never',4,fil['day_sleep'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
      <td>&lt;2</td>
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
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
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
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
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
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
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
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
      <td>&lt;2</td>
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




```python
fil['wake_up']=np.where(fil['wake_up']=='<2',0,fil['wake_up'])
fil['wake_up']=np.where(fil['wake_up']=='3',1,fil['wake_up'])
fil['wake_up']=np.where(fil['wake_up']=='4',2,fil['wake_up'])
fil['wake_up']=np.where(fil['wake_up']=='5',3,fil['wake_up'])
fil['wake_up']=np.where(fil['wake_up']=='>5',4,fil['wake_up'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>31 - 45</td>
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
      <td>10 pm - 12 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
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
      <td>10 pm - 12 am</td>
      <td>5-6</td>
      <td>0 - 15</td>
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
      <td>1 am</td>
      <td>7-8</td>
      <td>0 - 15</td>
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
      <td>Before 10 pm</td>
      <td>7-8</td>
      <td>0 - 15</td>
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




```python
fil['minutes_to_sleep']=np.where(fil['minutes_to_sleep']=='0 - 15',0,fil['minutes_to_sleep'])
fil['minutes_to_sleep']=np.where(fil['minutes_to_sleep']=='16 - 30',1,fil['minutes_to_sleep'])
fil['minutes_to_sleep']=np.where(fil['minutes_to_sleep']=='31 - 45',2,fil['minutes_to_sleep'])
fil['minutes_to_sleep']=np.where(fil['minutes_to_sleep']=='46 - 60',3,fil['minutes_to_sleep'])
fil['minutes_to_sleep']=np.where(fil['minutes_to_sleep']=='>60',4,fil['minutes_to_sleep'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
      <td>5-6</td>
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
      <td>10 pm - 12 am</td>
      <td>7-8</td>
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
      <td>10 pm - 12 am</td>
      <td>5-6</td>
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
      <td>1 am</td>
      <td>7-8</td>
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
      <td>Before 10 pm</td>
      <td>7-8</td>
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




```python
fil['no_of_hrs']=np.where(fil['no_of_hrs']=='<=4',0,fil['no_of_hrs'])
fil['no_of_hrs']=np.where(fil['no_of_hrs']=='5-6',1,fil['no_of_hrs'])
fil['no_of_hrs']=np.where(fil['no_of_hrs']=='7-8',2,fil['no_of_hrs'])
fil['no_of_hrs']=np.where(fil['no_of_hrs']=='>8',3,fil['no_of_hrs'])
```


```python
fil.head(5)
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
      <th>0</th>
      <td>20</td>
      <td>10 pm - 12 am</td>
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
      <td>10 pm - 12 am</td>
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
      <td>10 pm - 12 am</td>
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
      <td>1 am</td>
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
      <td>Before 10 pm</td>
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




```python
fil['time_sleep']=np.where(fil['time_sleep']=='Before 10 pm',0,fil['time_sleep'])
fil['time_sleep']=np.where(fil['time_sleep']=='10 pm - 12 am',1,fil['time_sleep'])
fil['time_sleep']=np.where(fil['time_sleep']=='1 am',2,fil['time_sleep'])
fil['time_sleep']=np.where(fil['time_sleep']=='After 1 am',3,fil['time_sleep'])
```


```python
fil.head(5)
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




```python
fil.dtypes
```




    age                       int64
    time_sleep               object
    no_of_hrs                object
    minutes_to_sleep         object
    wake_up                  object
    day_sleep                object
    tracker                  object
    use_tv                   object
    sleep_alone              object
    sep_sleep_place          object
    comfort                   int64
    perf                     object
    trouble_sleep            object
    trouble_back_to_sleep    object
    medication               object
    routine                  object
    rate                      int64
    gender                   object
    dtype: object




```python
for i in fil.columns.values:
        fil[i]=fil[i].apply(pd.to_numeric)
```


```python
fil.dtypes
```




    age                      int64
    time_sleep               int64
    no_of_hrs                int64
    minutes_to_sleep         int64
    wake_up                  int64
    day_sleep                int64
    tracker                  int64
    use_tv                   int64
    sleep_alone              int64
    sep_sleep_place          int64
    comfort                  int64
    perf                     int64
    trouble_sleep            int64
    trouble_back_to_sleep    int64
    medication               int64
    routine                  int64
    rate                     int64
    gender                   int64
    dtype: object


## Cleaned data 
```python
temp=fil
temp1=fil
temp2=fil
fil.to_csv('sleep_cleaned.csv',index=False)
```
## Normalization

```python
for i in temp.columns.values:
    temp[i] = temp[i] - temp[i].min(axis=0)
    temp[i] = temp[i]/(temp[i].max(axis=0)-temp[i].min(axis=0))
```


```python
temp.shape
temp.to_csv('sleep_norm_min.csv',index=False)
```


```python
for i in temp1.columns.values:
    temp1[i] = temp1[i] - temp1[i].max(axis=0)
    temp1[i] = temp[i]/(temp[i].max(axis=0)-temp[i].min(axis=0))
```


```python
temp1.shape
temp1.to_csv('sleep_norm_max.csv',index=False)
```


```python
for i in temp2.columns.values:
    temp2[i] = temp[i] - temp[i].mean(axis=0)
    temp2[i] = temp[i]/(temp[i].var(axis=0))
```


```python
temp1.shape
temp1.to_csv('sleep_norm_var.csv',index=False)
```
