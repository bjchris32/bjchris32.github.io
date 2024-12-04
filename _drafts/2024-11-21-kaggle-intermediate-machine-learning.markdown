---
layout: post
title:  "What I learned in Kaggle course - intermediate machine learning"
date:   2024-11-21
tags: [Machine Learning, kaggle, summary]
img: posts/machine-learning.webp
read_time: true
show_date: true
---

After completing Lesson 2 in the [Intermediate Machine Learning](https://www.kaggle.com/learn/intermediate-machine-learning/course) course on Kaggle, I categorized my learning journey into six problems.

### Problem 1: Handling Missing Values in Input Data

#### What did I learn?:
1. **Drop the columns with missing values**
    - **Cons:** This can lead to loss of valuable information and potential bias.
2. **Impute with mean value or other existing common value**
    - **Cons:** It may not always be clear which value to impute.
3. **Add an additional column to indicate imputation**

#### Tips:
- Remember to [add the columns and index](https://www.kaggle.com/code/anaslargab/ghosh-rakhi-s-fixed-notebook/comments#1771584) back after imputation.


## Problem 2:
How to represent categorical values? i.e. Male/Female, Colors

#### What did I learn?:
There are also three ways to handle categorial data.
1. Just drop it if the value is not that important.
    - **Cons:** This can lead to loss of valuable information and potential bias.
2. Ordinal Encoding: Use unique integers to represent different categorical values.
    - **Cons:** The categorical values should have inherent ranking or order, such as frequency never, sometimes, always.
3. One-Hot Encoding: Create additional columns for each unique categorical values. The values in the new columns will only be 0(present) or 1(not present).
    - **Cons:** Too many data -> sparse matrix

## Problem 3:
How to reduce duplication in preprocessing data?

#### What did I learn?:
Use pipeline to preprocess all kinds of data including training, validation and testing data.
Different library have different api to call, so just check the documentation later.

## Problem 4:
What is cross-validation?

#### What did I learn?:
To achieve best measures of model performance with limited dataset, we could make use of cross-validation.

#### How to do cross-validation?
1. Divide the dataset into multiple folds
2. Choose one of the fold as validation dataset
3. Get the score of the model
4. Back to step 2 until all folds of dataset are used as validation dataset


## Problem 5:
What is XGBoost?

#### What did I learn?:
To achieve best performance, we could iteratively add models to the current ensemble(original model).
I am still confused after reading kaggle's explanation. So, I asked ChatGPT to explain this concept to a 5-year-old:
>  Imagine you have a big box of LEGOs and you want to build the best LEGO tower ever. But instead of just stacking them up randomly, you have a super-smart friend who helps you build the tower step by step.
>
> Every time you add a piece to the tower, your friend checks if it looks good or wobbly. If it's wobbly, your friend fixes it by using a different LEGO piece. You keep doing this until the tower is super strong and looks awesome!
>
> Now, XGBoost is like that super-smart friend, but instead of building towers, it helps computers learn to make really good predictions by fixing mistakes step by step. It’s a tool that teaches computers to be really smart and make fewer errors, like figuring out if it’s going to rain or what toys you might like!

Now, I understood.

#### How to do XGBoost?
1. In a ensemble(original model), calculate the predictions from all models in the ensemble
2. Calculate a loss function with the predictions from step 1
3. Apply the loss function to a new model
4. Add the new model to original ensemble and back to step 1

## Problem 6:
How to identify Data leakage?

#### What did I learn?:
High accuracy in the prediction dataset may indicate data leakage. Data leakage occurs when prediction data or validation data is used in training model.

#### Tips:
* Be mindful of the time a column is calculated. Is this column calcuated after the prediction of some other dataset? For example, the average price of the same region when we're predicting the house price.
* remove one column of doubt to see if this column is the source of data leakage
