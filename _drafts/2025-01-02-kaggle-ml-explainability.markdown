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

### Problem 3: What is SHAP values?
Used to break down a prediction to show the impact of each feature
Some use cases, for example, are:
- A model says a bank shouldn't loan someone money, and the bank is legally required to explain the basis for each loan rejection
- A healthcare provider wants to identify what factors are driving each patient's risk of some disease so they can directly address those risk factors with targeted health interventions

#### What did I learn?
* Use the library to get the features that make positive or negative effect on the numeric prediction

* Summary Plots
  - width
  > The width of the effects range is not a reasonable approximation to permutation importance. For that matter, the width of the range doesn't map well to any intuitive sense of "importance" because it can be determined by just a few outliers. However if all dots on the graph are widely spread from each other, that is a reasonable indication that permutation importance is high. Because the range of effects is so sensitive to outliers, permutation importance is a better measure of what's generally important to the model.
  - jumbled/separated color
  > The jumbling suggests that sometimes increasing that feature leads to higher predictions, and other times it leads to a lower prediction. Said another way, both high and low values of the feature can have both positive and negative effects on the prediction. The most likely explanation for this "jumbling" of effects is that the variable (in this case num_lab_procedures) has an interaction effect with other variables. 

* SHAP contribution dependence plot
  - used when there is jumbled dots spread in summary plots. Set different "interaction_index" to see if there is any interaction between the feature with the other features.


