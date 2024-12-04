---
layout: post
title:  "What I learned in Kaggle course - intermediate machine learning summary"
date:   2024-11-21
tags: [Machine Learning]
img: posts/machine-learning.webp
read_time: true
show_date: true
---

## Context:
Lession 2 in [Intermediate Machine Learning](https://www.kaggle.com/learn/intermediate-machine-learning/course) of kaggle.

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
