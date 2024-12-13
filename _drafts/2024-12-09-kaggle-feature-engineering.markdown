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
> - Understand the features. Refer to your dataset's data documentation, if available.
> - Research the problem domain to acquire domain knowledge. If your problem is predicting house prices, do some research on real-estate for instance. Wikipedia can be a good starting point, but books and journal articles will often have the best information.
> - Study previous work. Solution write-ups from past Kaggle competitions are a great resource.
> - Use data visualization. Visualization can reveal pathologies in the distribution of a feature or complicated relationships that could be simplified. Be sure to visualize your dataset as you work through the feature engineering process.

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
> - Linear models learn sums and differences naturally, but can't learn anything more complex.
> - Ratios seem to be difficult for most models to learn. Ratio combinations often lead to some easy performance gains.
> - Linear models and neural nets generally do better with normalized features. Neural nets especially need features scaled to values not too far from 0. Tree-based models (like random forests and XGBoost) can sometimes benefit from normalization, but usually much less so.
> - Tree models can learn to approximate almost any combination of features, but when a combination is especially important they can still benefit from having it explicitly created, especially when data is limited.
> - Counts are especially helpful for tree models, since these models don't have a natural way of aggregating information across many features at once.


#### Tips:
- Be mindful of data leakage when creating aggregated feature. The aggregated feature should only be calculated from training dataset. In validation dataset, it should reuse the aggregated feature from the training dataset to avoid overfitting.

Simple example to explain data leakage again(cited from ChatGpt).
> Target Variable:
> We are trying to predict the Sales of a product based on features like the store (Store) and possibly derived features like the average sales of the store (Store_Avg_Sales).
>
> Features:
> Store: The store type where the product is sold.
> Store_Avg_Sales: The average sales of the store, which we compute as an aggregated feature.
>
> | ID | Store | Sales | Store_Avg_Sales |
> |----|-------|-------|-----------------|
> | 1  | A     | 200   | 210             |
> | 2  | A     | 220   | 210             |
> | 3  | B     | 150   | 145             |
> | 4  | B     | 140   | 145             |
> | 5  | A     | 210   | 210             |
> | 6  | B     | 145   | 145             |
>
> If Store_Avg_Sales is computed using the entire dataset (training + validation):
> The model sees an unrealistically informative feature for the validation set.
> For example:
> Row 5 (Store = A, Sales = 210) gets Store_Avg_Sales = 210, which already reflects its own Sales.
> The model can trivially predict Sales = 210 since the feature already "cheats."


### Problem 3: What are the features in unsupervised machine learning?
> In the context of feature engineering for prediction, you could think of an unsupervised algorithm as a "feature discovery" technique.
> ...
> Adding a feature of cluster labels can help machine learning models untangle complicated relationships of space or proximity.


### What did I learn?
* Why clustering?
When you apply clustering to your data, each data point is assigned a label that indicates which cluster it belongs to. That is, the lable became categorical feature. These labels can then be treated as categorical features in your dataset.

> The motivating idea for adding cluster labels is that the clusters will break up complicated relationships across features into simpler chunks. Our model can then just learn the simpler chunks one-by-one instead having to learn the complicated whole all at once. It's a "divide and conquer" strategy

We can cluster the dataset into chunks and train a model for each chuncks respectively. This way, we hope that the model of a chunk could be linear.

* What is K-means clustering?

> It's a simple two-step process. The algorithm starts by randomly initializing some predefined number (n_clusters) of centroids. It then iterates over these two operations:
>
> 1. assign points to the nearest cluster centroid
> 2. move each centroid to minimize the distance to its points
>
> It iterates over these two steps until the centroids aren't moving anymore, or until some maximum number of iterations has passed (max_iter).
>
> It often happens that the initial random position of the centroids ends in a poor clustering. For this reason the algorithm repeats a number of times (n_init) and returns the clustering that has the least total distance between each point and its centroid, the optimal clustering.
> Ordinarily though the only parameter you'll need to choose yourself is n_clusters (k, that is).

* How to apply K-means to create feature?
  * After K-means, use clustering label as a feature
  * An alternavive way with more granularity: After K-means, we can measure the distance between the data point to each centroid. These distances can be used as new features in your dataset, allowing you to provide more granular information about how the point relates to the various clusters rather than just indicating to which cluster it belongs.

#### Tips
- Since k-means clustering is sensitive to scale, it can be a good idea rescale or normalize data with extreme values.
> if the features are already directly comparable (like a test result at different times), then you would not want to rescale. On the other hand, features that aren't on comparable scales (like height and weight) will usually benefit from rescaling. Sometimes, the choice won't be clear though. In that case, you should try to use common sense, remembering that features with larger values will be weighted more heavily.
>
> Comparing different rescaling schemes through cross-validation can also be helpful.
