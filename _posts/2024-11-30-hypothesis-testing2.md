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

Here I would like to discuss the two-sample or independent t-test where we test two independent samples. To make it more clear we, will use the `scipy` library to conduct the t-test

As an example discussed in the previous section, we’ll test whether the average height of males in the US is different from those in the EU using Python. So the null hypothesis is that the population mean for the people in two regions are the same, and the alternative hypothesis is that the population mean for people in US are larger than those from EU.
Assume we have two datasets: one for the US and one for the EU.
$$H_0:\mu_{US}=\mu_{EU}$$  
$$H_A:\mu_{US}>\mu_{EU}$$  

An alternate way of writing the above equation is to compare the differences in population means to zero. Zero here corresponds to our hypothesized value for the differences in means.
$$H_0:\mu_{US}-\mu_{EU}=0$$  
$$H_A:\mu_{US}-\mu_{EU}>0$$  


```python
import numpy as np
from scipy.stats import ttest_ind

# Simulated heights (in cm) for males in the US and EU
us_heights = np.random.normal(loc=175, scale=8, size=100)  # Mean=175, SD=10
eu_heights = np.random.normal(loc=174, scale=8, size=100)  # Mean=170, SD=10
```

The distribution of these two height more or less looks the same, with almost the same mean. Now let's perform the t-test. For two-sample t-test we have consider the half of the p-value.

#### Standardizing test-statistic
The z-scores are calculated as follows,
\begin{equation}
z= \frac{Sample~stat-population~parameter}{SE}
\end{equation}
In the two sample case, the test statistic denoted as $$t$$, uses a similar equation
\begin{equation}
t= \frac{difference~in~sample~stat- difference~in~population~parameter}{SE}
\end{equation}

\begin{equation}
t= \frac{(\bar{x}_{US}-\bar{x}_{EU})- (\mu_{US}-\mu_{EU})}{SE(\bar{x}_{US}-\bar{x}_{EU})}
\end{equation}

The standard error is calculated as follows,
\begin{equation}
SE(\bar{x}_{US}-\bar{x}_{EU})\approx \sqrt{\frac{s^2_{US}}{n_{US}}+\frac{s^2_{EU}}{n_{EU}}}
\end{equation}

where $$s$$ is the standard deviation of the variable and $$n$$ is the sample size.
If we assume the null hypothesis is true:

$$H_0:\mu_{US}-\mu_{EU}=0 \implies t=\frac{(\bar{x}_{US}-\bar{x}_{EU})}{SE(\bar{x}_{US}-\bar{x}_{EU})}$$

$$t=\frac{(\bar{x}_{US}-\bar{x}_{EU})}{\sqrt{\frac{s^2_{US}}{n_{US}}+\frac{s^2_{EU}}{n_{EU}}}}$$


```python
xbar_us = us_heights.mean()
xbar_eu = eu_heights.mean()

s_us = us_heights.std()
s_eu = eu_heights.std()

us_n = len(us_heights)
eu_n = len(eu_heights)

print(xbar_us, xbar_eu)
177.97970220151245 170.06544972344068
print(s_us, s_eu)
7.967555003758265 7.834602080144636
print(us_n, eu_n)
3000 3000
```

Now let's calculate the test-statistic,

```python
# Calculate the numerator of the test statistic
numerator = xbar_us - xbar_eu

# Calculate the denominator of the test statistic
denominator = np.sqrt(s_us**2/us_n + s_eu**2/eu_n)

# Calculate the test statistic
t_stat = numerator/denominator

# Print the test statistic
print(t_stat)
38.793036979639794
```

```python
# Calculate the degrees of freedom
degrees_of_freedom = us_n + eu_n -2

# Calculate the p-value from the test stat
p_value = t.cdf(t_stat, df=degrees_of_freedom)

# Print the p_value
print(p_value)
```

The same procedure can be done in a easier way using the `scipy` library

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
