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
We have loaded a 

`@instructions`
- Instruction 1
- Instruction 2
- Instruction 3

`@hint`
- Here is the hint for this setup problem. 
- It should get students 50% of the way to the correct answer.
- So don't provide the answer, but don't just reiterate the instructions.
- Typically one hint per instruction is a sensible amount.

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
data_log_and_scaled[_:_]
```
`@solution`
```{python}
# Transform inputs to a log scale
data_log = np.log(datamart_kmeans)
# Standardize the data by centering and scaling
scaler = StandardScaler()
scaler.fit(data_log)
data_log_and_scaled = scaler.transform(data_log)
data_log_and_scaled[0:10]
```
`@sct`
```{python}
# Update this to something more informative.
success_msg("Some praise! Then reinforce a learning objective from the exercise.")
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

This is the assignment text. It should help provide students with the background information needed.
The instructions that follow should be in bullet point form with clear guidance for what is expected.

`@instructions`
- Instruction 1
- Instruction 2
- Instruction 3

`@hint`
- Here is the hint for this setup problem. 
- It should get students 50% of the way to the correct answer.
- So don't provide the answer, but don't just reiterate the instructions.
- Typically one hint per instruction is a sensible amount.

`@pre_exercise_code`
```{python}
import pandas as pd
from sklearn.cluster import KMeans

# Dataset that will be used is a numpy ndarray from previous exercise
data_log_and_scaled = data_log_and_scaled
```
`@sample_code`
```{python}
kmeans = KMeans(n_clusters=_, random_state=_).fit(_)
cluster_labels = kmeans._
datamart = datamart.assign(cluster = _)
datamart.groupby([_]).agg({
    _: _,
    _: _,
    _: 'mean',
    _: [_, _]
}).round(_)
```
`@solution`
```{python}
kmeans = KMeans(n_clusters=4, random_state=99).fit(data_log_and_scaled)
cluster_labels = kmeans.labels_
datamart = datamart.assign(cluster = cluster_labels)
datamart.groupby(['cluster']).agg({
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

