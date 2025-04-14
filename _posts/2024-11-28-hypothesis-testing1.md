---
layout: post
title: Hypothesis testing- Part I
date: 2024-11-28 15:04:00
description: Introduction to hypothesis testing
tags: statistics code
categories: ML-concepts
featured: false
# pretty_table: true
---

#### What is it?
Hypothesis testing is a fundamental statistical method used to validate claims or hypotheses. At its core, hypothesis testing aims to provide a structured approach to deciding whether there is enough evidence in a sample of data to support or reject a certain belief or claim about a population parameter.

## Null Hypothesis ($$H_0$$)
The **null hypothesis** represents the default or status quo assumption. It assumes no significant change between the variables you are testing. The form of null hypothesis varies from one scenario to test to another: if you are testing  a new drug, then the null hypothesis would be that the new drug has no effect.  For example, If you test the average height of male in US is greater than those in EU, the null hypothesis is that there is no difference.

## Alternative Hypothesis ($$H_1$$)
The purpose of hypothesis testing is to determine whether to reject or fail to reject the null hypothesis based on the gathered evidence. If there is little evidence against the null hypothesis, then we fail to reject the null hypothesis. If the null hypothesis is highly unlikely given the evidence, then we reject the null in favor of an alternative hypothesis $$H_{1}$$. The alternative hypothesis depends on the specific test. Considering the same example above, the alternative hypothesis would be that average height of male in US does in fact differ from those in EU.

## How Do We Make a Decision? Significance level and p-value
Once we define the null and alternative hypotheses, the next step is to assess the evidence so as to reject or fail to reject the null hypothesis. But how do we quantify this evidence in a way that allows for a clear and objective decision?
At the heart of this process is the concept of the **p-value** and the **significance level ($$\alpha$$)**.
To put in a mathematical perspective, we loot at the probability of obtaining the observed data under the assumption that  the null hypothesis is true. This probability threshold commonly called as significance level $$\alpha$$, determines whether to reject the null hypothesis when the null hypothesis is true (Type I error). A common value for $$\alpha$$ is $$5\%$$. This means that there a $$5\%$$ risk of rejecting the null hypothesis. i.e. believing there is a difference in the observed evidence when there actually isn't.

> The **p-value** is the probability of observing the data—or something more extreme—assuming that the null hypothesis is true.

**p-value**provides a measure of how compatible the data is with the null hypothesis. A smaller p-value indicates that the observed data is less likely under the null hypothesis, providing stronger evidence against it. Now what p-values rejects the null hypothesis. For this there's a threshold that we set based on specific circumstances.

> The **significance level ($$\alpha$$)** is a threshold we set in advance to determine whether the p-value is small enough to reject the null hypothesis. In essence, $$\alpha$$ defines the maximum probability of making a **Type I error**—rejecting the null hypothesis when it is actually true.

The significance level represents our tolerance for risk in making an incorrect conclusion. A common value for $$\alpha$$ is **0.05** (or 5%), although it can vary depending on the context. For example:

- In medical research, where making a false claim about a treatment's effectiveness can have serious consequences, $$\alpha$$ might be set to a stricter level, such as 0.01.
- In exploratory research, where the goal is to identify potential leads rather than make definitive claims, $$\alpha$$ might be set to 0.1.

If we choose $$\alpha = 0.05$$, this means there is a **5% risk of rejecting the null hypothesis when it is actually true**. In other words, we are allowing for a 5% chance of observing results as extreme as those in the data (or more extreme) due to random sampling variability, even though the null hypothesis is correct.

Another way to make a decision is using the test statistic. A test statistic is defined as a quantity taken from a sample that is used for deciding whether to reject or accept the null hypothesis.
The general formula for calculating a test statistic is:

$$
test~statistic = \frac{Sample ~ statistic-Value ~ of ~ parameter~ according~to ~null}{Standard~error~(SE)~of~the~sample~statistic}
$$

If the test-statistic is greater than the critical value then we reject the null hypothesis and vice-versa.

### Role of the p-Value in Decision-Making

To decide whether to reject the null hypothesis, we compare the p-value to the significance level $$\alpha$$:
- If the **p-value ≤ $$\alpha$$**, we **reject the null hypothesis**. This indicates that the data provides sufficient evidence to conclude that the null hypothesis is unlikely to be true.
- If the **p-value > $$\alpha$$**, we **fail to reject the null hypothesis**. This means the data does not provide strong enough evidence against the null hypothesis, so we retain it (but we do not prove it to be true).

## Balancing Significance Level and Risk

Choosing the significance level is a trade-off between sensitivity and specificity. Lowering $$\alpha$$ (e.g., from 0.05 to 0.01) reduces the risk of Type I errors but increases the risk of **Type II errors** (failing to reject the null hypothesis when it is false). The choice of $$\alpha$$ depends on the context and the consequences of making incorrect decisions.

By combining the p-value with a carefully chosen significance level, hypothesis testing provides a rigorous and systematic way to assess the evidence, helping researchers make data-driven conclusions with confidence.
Now that's about the basic understanding of hypothesis testing. There are several statistical test available based on the nature of the data and the objective of the test. Some common types include:
1. **One-Sample T-Test**: Tests whether the mean of a single sample differs from a known value.
2. **Two-Sample T-Test**: Compares the means of two independent samples.  
3. **Paired T-Test**: Compares means from the same group at different times.  
4. **Chi-Square Test**: Tests the association between categorical variables.  
5. **ANOVA (Analysis of Variance)**: Compares means among three or more groups.

In the next part we will look at some of the commonly used statistical test.
