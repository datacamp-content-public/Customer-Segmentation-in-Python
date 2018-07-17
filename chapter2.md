---
title       : Cohort Analysis
description : Insert the chapter description here

---
## Capstone Exercise

```yaml
type: NormalExercise
lang: python
xp: 100
skills: 2
key: 16f6ff0c7d

```
This is the assignment text. It should help provide students with the background information needed.
The instructions that follow should be in bullet point form with clear guidance for what is expected.

**Learning objective:** Calculate the average monthly spend for Quantity-based cohorts

You are given a transcational dataset we used in the exercises previously with all transactions, cohort month and cohort index calculated:
['InvoiceNo', 'Quantity', 'CustomerID', 'TotalSum', 'CohortMonth', 'CohortIndex']

You will follow the same steps we have completed for the time-based and size-based cohorts in the lectures. 

`@instructions`
- Instruction 1 - Calculate total `Quantity` purchased for each customer in their first month
- Instruction 2 - Create a new column that calculates quartiles based on first month's `Quantity` and append it to `data`
- Instruction 3 - Calculate average spend for each cohort monthly and create a pivot 
- Instruction 4 - Plot the heatmap by passing the `quantity_cohorts` dataset to the function

`@hint`
- Here is the hint for this setup problem. 
- It should get students 50% of the way to the correct answer.
- So don't provide the answer, but don't just reiterate the instructions.
- Typically one hint per instruction is a sensible amount.

`@pre_exercise_code`
```{python}
# Load datasets and packages here.

import pandas as pd
import seaborn as sns
data = pd.read_excel('Capstone_1_Data.xlsx')

```
`@sample_code`
```{python}
# Calculate total Quantity purchased for each customer in their first month
q_data = data[data['_'] == _].groupby([_])[_].agg(_).reset_index()
# Create a new column that calculates quartiles based on first month's Quantity
q_data = q_data.assign(QuantityQuartile = pd.qcut(x=q_data[_], q=_, labels = range_, _) ))
# Append the quartile values back to the original dataset
data = data.merge(q_data[[_, _]], on=_, how=_).reset_index()
# Calculate average spend for each cohort monthly
q_agg = data.groupby([_, _])[_].mean()
# Pivot the aggregated dataset so that Quartile values are in rows, and Cohort index is in columns 
q_cohorts = q_agg.reset_index().pivot(index_, columns=_, values=_)
# Plot the heatmap 
plt.figure(figsize=(12, 3)); plt.title('Average Spend by Quantity quartiles')
sns.heatmap(_, annot=True, fmt='.1f', cmap='Blues')
plt.show()
```
`@solution`
```{python}
# Calculate total Quantity purchased for each customer in their first month
q_data = data[data['CohortIndex'] == 1].groupby(['CustomerID'])['Quantity'].agg('sum').reset_index()
# Create a new column that calculates quartiles based on first month's Quantity
q_data = q_data.assign(QuantityQuartile = pd.qcut(x=q_data['Quantity'], q=4, labels = range(1,5) ))
# Append the quartile values back to the original dataset
data = data.merge(q_data[['CustomerID', 'QuantityQuartile']], on='CustomerID', how='left').reset_index()
# Calculate average spend for each cohort monthly
q_agg = data.groupby(['QuantityQuartile', 'CohortIndex'])['TotalSum'].mean()
# Pivot the aggregated dataset so that Quartile values are in rows, and Cohort index is in columns 
q_cohorts = q_agg.reset_index().pivot(index='QuantityQuartile', columns='CohortIndex', values='TotalSum')
# Plot the heatmap 
plt.figure(figsize=(12, 3)); plt.title('Average Spend by Quantity quartiles')
sns.heatmap(q_cohorts, annot=True, fmt='.1f', cmap='Blues')
plt.show()
```
`@sct`
```{python}
# Update this to something more informative.
success_msg("Some praise! Then reinforce a learning objective from the exercise.")
```




