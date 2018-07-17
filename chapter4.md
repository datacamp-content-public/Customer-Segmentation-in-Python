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

We have now successfully built RFM segments based on quartile values of recency, frequency and monetary value. Now, you will build 

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
Tquartiles = pd.qcut(data['Tenure'], 4, labels = list(reversed(range(1,5))))
data = data.assign(T = Tquartiles.values)
top_recency = data[data['M']==1]
monetary = top_recency.groupby(['RFMScore', 'T'])['CustomerID'].nunique().reset_index()
mypivot = monetary.pivot(index='RFMScore', columns='T', values='CustomerID')
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




