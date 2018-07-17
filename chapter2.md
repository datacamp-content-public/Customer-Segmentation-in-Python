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
**Learning objective:** Calculate the average monthly spend for Quantity-based cohorts

You are given a transcational dataset we used in the exercises previously with all transactions, cohort month and cohort index calculated:
**InvoiceNo,Quantity,CustomerID,TotalSum,CohortMonth,CohortIndex**

You will follow the same steps we have completed for the time-based and size-based cohorts in the lectures. 

`@instructions`
- Instruction 1 - Calculate total `Quantity` purchased for each customer in their first month
- Instruction 2 - Create a new column that calculates quartiles based on first month's `Quantity` and append it to `data`
- Instruction 3 - Calculate average spend for each cohort monthly and create a pivot 
- Instruction 4 - Plot the heatmap by passing the `quantity_cohorts` dataset to the function

`@hint`
- Did you filter out the first cohort index, and have the correct values in the `groupby` clause?
- Make sure your number of quantiles is 4, and your range starts counting from 1
- Have you used `TotalSum` for the average spend? Also, check if your `pivot` call has the right values
- Have you passed the pivotted dataset to the `heatmap` function call?

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
q_data = data[data[_] == _].groupby([_])[_].agg(_).reset_index()
# Create a new column that calculates quartiles based on first month's Quantity
q_data = q_data.assign(QuantityQuartile = pd.qcut(x=q_data[_], q=_, labels = range(_, _) ))
# Append the quartile values back to the original dataset
data = data.merge(q_data[[_, _]], on=_, how=_).reset_index()
# Calculate average spend for each cohort monthly
q_agg = data.groupby([_, _])[_].mean().reset_index()
# Pivot the aggregated dataset so that Quartile values are in rows, and Cohort index is in columns 
q_cohorts = q_agg.pivot(index_, columns=_, values=_)
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
q_agg = data.groupby(['QuantityQuartile', 'CohortIndex'])['TotalSum'].mean().reset_index()
# Pivot the aggregated dataset so that Quartile values are in rows, and Cohort index is in columns 
q_cohorts = q_agg.pivot(index='QuantityQuartile', columns='CohortIndex', values='TotalSum')
# Plot the heatmap 
plt.figure(figsize=(12, 3)); plt.title('Average Spend by Quantity quartiles')
sns.heatmap(q_cohorts, annot=True, fmt='.1f', cmap='Blues')
plt.show()
```
`@sct`
```{python}
# Update this to something more informative.
success_msg("Congratulations! You have now mastered cohort analysis and are ready to dig deep into your data!")
```




