---
title       : Customer Segmentation with K-means clustering
description : Use data from previous chapter to build customer segments based on their recency, frequency, and monetary value

---
## Capstone Exercise 1.1

```yaml
type: NormalExercise
lang: python
xp: 100
skills: 2
key: 16f6ff0c7d

```
We have loaded different data for the same customers as `datamart_kmeans`. You will find three varialbes for each `CustomerID`: `FrequencyMonthly`, `PriceAverage`, and `Tenure`.

Now, you job will be to first pre-process the data as in the lectures - transform it to the log scale, and scale it. 

In the next part of this exercise you will cluster the customer using this data and then identify most valuable segments.

`@instructions`
- Transform the `datamart_kmeans` dataset on a log scale, and store to `data_log`
- Fit the intialized scaler with the log-transformed data
- Transform the data to a scaled version and store it to `data_log_and_scaled`
- Finally, print the top 10 rows of the transformed dataset

`@hint`
- Have you passed the loaded dataset to the `log` function?
- Make sure the log-scaled data is passed to the `fit` method of the `scaler`
- This function expects the same log-scaled data as in the previous step
- Are you sure you are only printing 10 rows?

`@pre_exercise_code`
```{python}
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler

datamart_kmeans = pd.read_excel('datamart_kmeans.xlsx')
print(datamart_kmeans[:5])
```
`@sample_code`
```{python}
# Transform inputs to a log scale
data_log = np.log(_)
# Standardize the data by centering and scaling
scaler = StandardScaler()
scaler.fit(_)
data_log_and_scaled = scaler.transform(_)
print(data_log_and_scaled[_:_])
```
`@solution`
```{python}
# Transform inputs to a log scale
data_log = np.log(datamart_kmeans)
# Standardize the data by centering and scaling
scaler = StandardScaler()
scaler.fit(data_log)
data_log_and_scaled = scaler.transform(data_log)
print(data_log_and_scaled[0:10])
```
`@sct`
```{python}
# Update this to something more informative.
success_msg("Great job! We are now ready to use this data for building customer segments with K-means clustering!")
```

---
## Capstone Exercise 1.2

```yaml
type: NormalExercise
lang: python
xp: 100
skills: 2
key: 2de4591a58
```

You will now build four customer segments with K-means clustering on previously pre-processed `FrequencyMonthly`, `PriceAverage`, and `Tenure` variables.

Finally, we will analyze the average values of these variables for each segment.

We have loaded the `data_log_and_scaled` from your previous exercise, together with `online_kmeans` dataset which has original `FrequencyMonthly`, `PriceAverage`, and `Tenure` variables, together with `MonetaryValue` data.

`@instructions`
- Initialize `KMeans` with four cluster, random state of 99 and pass the log-scaled data to the `fit` function
- Store cluster labels to `cluster_labels` dataset and create a new `cluster` column in the `online_kmeans` dataset by passing previously saved labels
- Finally, aggregate the dataset by the `cluster`, and calculate average values for each of the four variables, plus - pass `count` to the last one to get the number of customers as a last column.

`@hint`
- Here is the hint for this setup problem. 
- It should get students 50% of the way to the correct answer.
- So don't provide the answer, but don't just reiterate the instructions.
- Typically one hint per instruction is a sensible amount.

`@pre_exercise_code`
```{python}
import pandas as pd
from sklearn.cluster import KMeans

data_log_and_scaled = pd.read_excel('kmeans_data_logscaled.xlsx')
online_kmeans = pd.read_excel('online_kmeans.xlsx')
```
`@sample_code`
```{python}
kmeans = KMeans(n_clusters=_, random_state=_).fit(_)
cluster_labels = kmeans._
online_kmeans = online_kmeans.assign(cluster = _)
online_kmeans.groupby([_]).agg({
    _: _,
    _: _,
    _: _,
    _: [_, _]
}).round(_)
```
`@solution`
```{python}
kmeans = KMeans(n_clusters=4, random_state=99).fit(data_log_and_scaled)
cluster_labels = kmeans.labels_
online_kmeans = online_kmeans.assign(cluster = cluster_labels)
online_kmeans.groupby(['cluster']).agg({
    'FrequencyMonthly': 'mean',
    'PriceAverage': 'mean',
    'Tenure': 'mean',
    'MonetaryValue': ['mean', 'count']
}).round(1)
```
`@sct`
```{python}
# Update this to something more informative.
success_msg("Some praise! Then reinforce a learning objective from the exercise.")
```

