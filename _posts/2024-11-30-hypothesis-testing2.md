---
layout: post
title: Hypothesis testing- Part II- t-test
date: 2024-11-30 15:04:00
description: two-sample t-test for hypothesis testing
tags: statistics code
categories: ML-concepts
featured: false
# pretty_table: true
---

For most of the blogs I read, the null and alternative hypothesis were discussed based on the population mean and the sample mean. To test the hypothesis one can use one-sample t-test. But here I would like to discuss the two-sample or independent t-test where we test two independent samples. To make it more clear we use the `scipy` library to conduct the t-test
As an example discussed above, we’ll test whether the average height of males in the US is different from those in the EU using Python. Assume we have two datasets: one for the US and one for the EU.

```python
import numpy as np
from scipy.stats import ttest_ind

# Simulated heights (in cm) for males in the US and EU
us_heights = np.random.normal(loc=175, scale=8, size=100)  # Mean=175, SD=10
eu_heights = np.random.normal(loc=174, scale=8, size=100)  # Mean=170, SD=10
```

The distribution of these two height more or less looks the same, with almost the same mean. Now let's perform the t-test. For two-sample t-test we have consider the half of the p-value.
```python
# Perform an independent t-test
t_stat, p_value = ttest_ind(us_heights, eu_heights)

# Set significance level
alpha = 0.05

# Output results
print(f"T-statistic: {t_stat}")
print(f"P-value: {p_value}")

if p_value/2 < alpha:
    print("We reject the null hypothesis. There is a significant difference in average heights.")
else:
    print("We fail to reject the null hypothesis. There is no significant difference in average heights.")
```
output:
`T-statistic: 40.020422168327485`
`P-value: 0.0`
`We reject the null hypothesis. There is a significant difference in average heights.`
`t-critical:1.6451077126390887`


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/height_distribution2.png" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/t-distribution2.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
