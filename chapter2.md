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

import pandas as pd
import seaborn as sns

data = pd.read_excel('Capstone_1_Data.xlsx')

```
`@sample_code`
```{python}
# Calculate total Quantity purchased for each customer in their first month
quantity_data = data[data['_'] == _].groupby([_])[_].agg(_).reset_index()

# Create a new column that calculates Quantity Quartile
quantity_data = quantity_data.assign(QuantityQuartile = pd.qcut(x=quantity_data[_], q=_, labels = range_, _) ))

# Append the quartile value back to the original dataset
data = data.merge(quantity_data[[_, _]], on=_, how=_).reset_index()

# Calculate average spend for each cohort monthly
quantity_agg = data.groupby([_, _])[_].mean()

# Pivot the aggregated dataset 
quantity_cohorts = quantity_agg.reset_index().pivot(index_, columns=_, values=_)

# Plot the heatmap 
plt.figure(figsize=(12, 3))
plt.title('Average Spend by Quantity quartiles')
sns.heatmap(_, annot=True, fmt='.1f', cmap='Blues')
plt.show()
```
`@solution`
```{python}
# Calculate total Quantity purchased for each customer in their first month
quantity_data = data[data['CohortIndex'] == 1].groupby(['CustomerID'])['Quantity'].agg('sum').reset_index()

# Create a new column that calculates Quantity Quartile
quantity_data = quantity_data.assign(QuantityQuartile = pd.qcut(x=quantity_data['Quantity'], q=4, labels = range(1,5) ))

# Append the quartile value back to the original dataset
data = data.merge(quantity_data[['CustomerID', 'QuantityQuartile']], on='CustomerID', how='left').reset_index()

# Calculate average spend for each cohort monthly
quantity_agg = data.groupby(['QuantityQuartile', 'CohortIndex'])['TotalSum'].mean()

# Pivot the aggregated dataset 
quantity_cohorts = quantity_agg.reset_index().pivot(index='QuantityQuartile', columns='CohortIndex', values='TotalSum')

# Plot the heatmap 
plt.figure(figsize=(12, 3))
plt.title('Average Spend by Quantity quartiles')
sns.heatmap(quantity_cohorts, annot=True, fmt='.1f', cmap='Blues')
plt.show()
```
`@sct`
```{python}
# Update this to something more informative.
success_msg("Some praise! Then reinforce a learning objective from the exercise.")
```




