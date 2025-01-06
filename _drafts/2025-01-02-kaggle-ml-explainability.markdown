---
layout: post
title:  "What I learned in Kaggle course - Machine Learning Explainability"
date:   2024-12-09
tags: [Machine Learning, kaggle, summary]
img: posts/machine-learning.webp
read_time: true
show_date: true
---

## Why do we need to explain feature in machine learning?
We need the answer to the question:
> What features have the biggest impact on predictions?

### Problem 1: Why permutation importance?
> - fast to calculate,
> - widely used and understood, and
> - consistent with properties we would want a feature importance measure to have.


#### What did I learn?:
* How do we get the feature importance?
> If I randomly shuffle a single column of the validation data, leaving the target and all other columns in place, how would that affect the accuracy of predictions in that now-shuffled data
1. Get a trained model
2. Shuffle one column, calculate the loss and measure how much performance deteriation from the shuffling
3. Reverse previous shuffle and iterate another column until we calculate all importance



