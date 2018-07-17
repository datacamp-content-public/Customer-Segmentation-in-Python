---
title       : Market Basket Analysis
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
import pandas as pd
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules

basket = pd.read_excel('BasketFR.xlsx')
```
`@sample_code`
```{python}

```
`@solution`
```{python}
apriori_data = apriori(basket, min_support=0.01, use_colnames=True)
arules = association_rules(apriori_data, min_threshold=10.0, metric='lift')
top5_lift = arules[arules['support']>0.025].sort_values(by=['lift'], ascending=False)[0:5]
top5_lift
```
`@sct`
```{python}
# Update this to something more informative.
success_msg("Some praise! Then reinforce a learning objective from the exercise.")
```




