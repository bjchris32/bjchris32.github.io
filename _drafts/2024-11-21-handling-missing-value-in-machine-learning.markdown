---
layout: post
title:  "handling missing values in machine learning"
date:   2024-11-21
tags: [Machine Learning]
img: posts/machine-learning.webp
read_time: true
show_date: true
---

## Context:
Lession 2 in [Intermediate Machine Learning](https://www.kaggle.com/learn/intermediate-machine-learning/course) of kaggle.

## Problem:
There would be missing values in input data.

## Solution:
* drop the columns with missing values
    * cons: deviation
* impute with mean value or other existing common value
    * not sure which value to impute
* additional column to indicate imputation

## Tips
* remember to add the columns and index back after imputation
