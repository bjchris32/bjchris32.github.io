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

### Problem 2: How to create (useful) features?
> Understand the features. Refer to your dataset's data documentation, if available.
> Research the problem domain to acquire domain knowledge. If your problem is predicting house prices, do some research on real-estate for instance. Wikipedia can be a good starting point, but books and journal articles will often have the best information.
> Study previous work. Solution write-ups from past Kaggle competitions are a great resource.
> Use data visualization. Visualization can reveal pathologies in the distribution of a feature or complicated relationships that could be simplified. Be sure to visualize your dataset as you work through the feature engineering process.

#### What did I learn?:
- several ways to create features:
  - mathematical formula
  - string composition or decomposition
  - aggregation
    - count
    - mean
    - min
    - median, etc

- Guidelines about when to use which method:
> Linear models learn sums and differences naturally, but can't learn anything more complex.
> Ratios seem to be difficult for most models to learn. Ratio combinations often lead to some easy performance gains.
> Linear models and neural nets generally do better with normalized features. Neural nets especially need features scaled to values not too far from 0. Tree-based models (like random forests and XGBoost) can sometimes benefit from normalization, but usually much less so.
> Tree models can learn to approximate almost any combination of features, but when a combination is especially important they can still benefit from having it explicitly created, especially when data is limited.
> Counts are especially helpful for tree models, since these models don't have a natural way of aggregating information across many features at once.


#### Tips:
- Be mindful of data leakage when creating aggregated feature. The aggregated feature should only be calculated from training dataset. In validation dataset, it should reuse the aggregated feature from the training dataset to avoid overfitting.