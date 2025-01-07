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

### Problem 2: Why partial dependence plots?
Explain a feature affects predictions.
For example,
> Controlling for all other house features, what impact do longitude and latitude have on home prices? To restate this, how would similarly sized houses be priced in different areas?

#### What did I learn?

* Why not coefficient?
> partial dependence plots on sophisticated models can capture more complex patterns than coefficients from simple models.

Partial dependence plots are a way to visualize the relationship between a specific feature (or variable) and the predicted outcome of a model, while accounting for the average effects of all other features. They help us understand how changes in one variable affect predictions, independent of other variables.

* How does PDP work?
1. Start with a specific observation (a row of data). Say, a player with ball possession, shots, and goals. The model is designed to predict target: the man of the match.
2. Then, systematically change one feature (e.g., ball possession) while keeping the other features constant. You might predict the outcome for different value of ball possession.
3. Make prediction. For each of these altered values, you use the fitted model to predict the outcome (probability of winning "man of the match"). You plot these predictions on the vertical axis against the varying values of ball possession on the horizontal axis.
4. Averaging Over Multiple Rows. A single row might not capture the overall effect (due to interactions with other features), you repeat the process for many rows in your dataset. For each value of ball possession, you average the predicted outcomes.
  - Set the ball possession to the value of our interest, which is why the plot is called "partial".
  - Gather predictions from all teams.
  - Calculate the average from these predictions.

* How to observe the interactions between features?
Use 2D Partial Dependence Plots

* From the exercise, we learned that a feature with steep partial dependence does not garantee high permutation importance, and vice versa.

#### Pending/TODO
* From the exercise, I still did not grasp the concept of how to set the feature and target, such that it will have steep partial dependence or flat partial dependence. Maybe more real world use cases would better explain them than the mathametic functions.

* check out the thread/clips here:
  - https://www.kaggle.com/discussions/getting-started/65782
  - https://www.youtube.com/watch?v=uQQa3wQgG_s&ab_channel=ritvikmath

