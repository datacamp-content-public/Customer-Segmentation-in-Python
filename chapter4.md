---
title       : Recency, Frequency, Monetary Value analysis
description : Learn how to use simple rule-based segmentation to understand and segment the customers

---
## Capstone Exercise

```yaml
type: NormalExercise
lang: python
xp: 100
skills: 2
key: 16f6ff0c7d
```

We have successfully built RFM segments based on quartile values of recency, frequency and monetary value. Now, you will build quartiles based on a fourth metric of `Tenure`. Then, you will select the customers in the highest `MonetaryValue` quartile. Finally, you will then count the number of customers in the remaining dataset grouped by tenure quartiles and RFM scores. Your goal will be to identify the largest customer groups to select for targeting in a customized marketing campaign.

`@instructions`
- Create quartile values based on `Tenure` variable and pass it as a new column in `data`.
- Filter out top 1 Monetary value quartile and store the result to `top_recency` dataset.
- Count the number of unique customers in each RFM score and Tenure quartile combination and store to `monetary` dataset.
- Pivot the results from previous task with RFM Score in rows and Tenure quartiles in columns, use the customer count as values.

`@hint`
- Quartiles are four groups of equal size. Make sure labels start from 1.
- Are you using monetary quartile column, and filtering the top one only?
- Have you used `nunique()` function to count customers?
- Have you passed the right variables to `index`, `column`, and `values`?

`@pre_exercise_code`
```{python}
import pandas as pd
data = pd.read_excel('RFM-Datamart.xlsx')
```
`@sample_code`
```{python}
Tquartiles = pd.qcut(x=data[_], q=_, labels = list(reversed(range(_, _))))
data = data.assign(T = _.values)
top_recency = data[data[_]==_]
monetary = top_recency.groupby([_, _])[_]._.reset_index()
mypivot = monetary.pivot(index=_, columns=_, values=_)
print(mypivot)

```
`@solution`
```{python}
Tquartiles = pd.qcut(data['Tenure'], 4, labels = list(reversed(range(1,5))))
data = data.assign(T = Tquartiles.values)
top_recency = data[data['M']==1]
monetary = top_recency.groupby(['RFMScore', 'T'])['CustomerID'].nunique().reset_index()
mypivot = monetary.pivot(index='RFMScore', columns='T', values='CustomerID')
print(mypivot)

```
`@sct`
```{python}
# Update this to something more informative.
success_msg("Some praise! Then reinforce a learning objective from the exercise.")
```




