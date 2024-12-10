---
layout: post
title:  "What I learned in Kaggle course - feature engineering"
date:   2024-12-09
tags: [Machine Learning, kaggle, summary]
img: posts/machine-learning.webp
read_time: true
show_date: true
---

## Why do we need feature engineering?
> For a feature to be useful, it must have a relationship to the target that your model is able to learn.

Feature engineering is a process to transform the features to make their relationship to the target.
Problem is:

> how do you identify features in the dataset that might be useful to combine?

### Problem 1: What is Mutual Information(MI)?
> What we're calling uncertainty is measured using a quantity from information theory known as "entropy". The entropy of a variable means roughly: "how many yes-or-no questions you would need to describe an occurance of that variable, on average." The more questions you have to ask, the more uncertain you must be about the variable. Mutual information is how many questions you expect the feature to answer about the target.


#### What did I learn?:
- MI can help you to understand the relative potential of a feature as a predictor of the target. MI can't detect interactions between features. It is a univariate metric.
- The actual usefulness of a feature depends on the model you use it with.


#### Tips:
- Pick the features with high MI. Beyond that, if there is any low MI feature have interaction with high MI features, we could take this low MI feature into consideration - i.e. there are some distinctions in trend between target and high MI feature, given different value of low MI feature.
