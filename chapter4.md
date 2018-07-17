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
# Load datasets and packages here.
print('Hello, DataCamp!')
```
`@sample_code`
```{python}
Tquartiles = pd.qcut(x=data[_], q=_, labels = list(reversed(range(_, _))))
data = data.assign(T = Tquartiles.values)
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




