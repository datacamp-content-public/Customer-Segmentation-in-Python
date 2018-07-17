---
title       : Market Basket Analysis
description : Explore association rules between products that are purchased together

---
## Capstone Exercise

```yaml
type: NormalExercise
lang: python
xp: 100
skills: 2
key: 16f6ff0c7d
```

We have loaded a one-hot-encodded orders dataset with invoice numbers in the rows, and product names in the columns. The values in the table are either 1 or 0, depending whether the product was in the order, or not. This dataset contains orders from France, in contrast to the previous example where orders were generated in Germany. Let's see if we can find meaningul and interesting market basket rules.

`@instructions`
- Run `apriori` function on the `basket` dataset with minimum support threshold at 0.01, store the result to `apriori_data`.
- Pass the results from previous command to `association_rules` function, and use the `lift` as the threshold with minimum value of 2.0.
- Create a new dataset `top5_lift` with rules that have `support` higher than 0.04, and values sorted by `lift` measure. Then, select top 5 values.
- Finally, print the top five largest-lift rules.

`@hint`
- Have you passed `basket` dataset to the function, and defined the `min_support` value? 
- Make sure you enter both the metric name, as well as the actual threshold.
- It's important that you first filter out the rules by `support`, then sort them by `lift` in a descending manner. Finally, filter out top 5 rows.

`@pre_exercise_code`
```{python}
import pandas as pd
from mlxtend.frequent_patterns import apriori
from mlxtend.frequent_patterns import association_rules

basket = pd.read_excel('BasketFR.xlsx')
```
`@sample_code`
```{python}
apriori_data = apriori(_, min_support=_, use_colnames=True)
arules = association_rules(_, min_threshold=_, metric=_)
top5_lift = arules[arules['support']>_].sort_values(by=[_], ascending=_)[0:_]
print(top5_lift)
```
`@solution`
```{python}
apriori_data = apriori(basket, min_support=0.01, use_colnames=True)
arules = association_rules(apriori_data, min_threshold=2.0, metric='lift')
top5_lift = arules[arules['support']>0.04].sort_values(by=['lift'], ascending=False)[0:5]
print(top5_lift)
```
`@sct`
```{python}
# Update this to something more informative.
success_msg("Fantastic! You have now identified the market basket rules in France with highest lift - what do they tell you?")
```




