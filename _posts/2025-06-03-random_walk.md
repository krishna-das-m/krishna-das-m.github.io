---
layout: post
title: Random Walks- From Drunkard's Steps to Financial Markets
date: 2025-05-18 15:04:00
description: Defining the network architecture and intializing the NN parameters
tags: ML
categories: ML-concepts
featured: false
# pretty_table: true
---
Random walks are among the most fundamental and elegant concepts in probability theory, with applications spanning from physics and biology to finance and computer science. At its core, a random walk describes a mathematical model where a particle or entity moves through space in a sequence of random steps.

## What is a Random Walk?

Imagine a person standing on a number line at position zero. At each time step, they flip a coin: heads means they take one step to the right (+1), tails means they take one step to the left (-1). After many coin flips, their position traces out what mathematicians call a simple random walk.

More formally, a random walk is a sequence of positions $$S_0$$, $$S_1$$, $$S_2$$, ... where:

$$S_0 = 0$$ (starting position)

$$S_n = S_0 + X_1 + X_2 + ... + X_n$$

Here, each $$X_i$$ represents a random step, and the position at time n is simply the sum of all previous steps.

Let's implement a simple random walk in Python:
```python
import numpy as np

def simple_random_walk(n_steps=100, n_dims=2):
    """Generate a simple random walk."""
    steps = np.random.choice([-1,0, 1], size=(n_steps, n_dims))
    origins = np.zeros((1, n_dims))
    paths = np.cumsum( steps, axis=0)
    paths = np.concatenate((origins, paths), axis=0)
    return paths
```
<div class="row justify-content-center">
    <div class="col-sm-8 col-md-6 mt-4">
        {% include figure.liquid loading="eager" path="assets/img/blog/random_walk_2d.gif" class="img-fluid rounded z-depth-1" style="max-width: 300px; height: auto;" %}
    </div>
</div>

## Unbiased Random Walks

An unbiased random walk (also called a symmetric random walk) is one where each step has equal probability in all possible directions. In the simplest one-dimensional case:
- $$P(step=+1)=1/2$$
- $$P(step=-1)=1/2$$
The expected value of each step is zero: $$E[X_i]=(+1)\times (1/2) + (-1)\times (1/2)=0$$

<div class="row justify-content-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/blog/2d_random_walks_animated.gif" class="img-fluid rounded z-depth-1" style="max-width: 300px; height: auto;" %}
    </div>
</div>

## Biased random walks

A biased random walk introduces a drift or tendency to move in a particular direction. Instead of equal probabilities, we might have:
- $$P(step=+1)=p$$
- $$P(step=-1)=q=1-p$$

When $$p \neq 1/2$$, the walk becomes biasd. The expected value of each step is now $$E[X_i]=(+1)\times p + (-1)\times (1-p)=2p-1$$
