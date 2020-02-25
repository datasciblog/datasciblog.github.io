---
layout: single
title:  "Tree-Boosting-03: Tree Boosting With XGBoost - Why Does XGBoost Win "Every" Machine Learning Competition?"
date:   2020-02-26
permalink: /2020/02/26/tree-boosting-03/
excerpt: ""
categories: 
- Machine Learning
tags:
- tree-based
- boosting
- ensemble
- algorithm
- xgboost
classes: wide
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

# Introduction

- In this part of the series Tree Boosting, we have already talked about the basics of decision trees which are used as base leaners of tree boosting algorithms. We also discuss several approaches of building ensembling models from decision trees such as bagging, random forests and boosting.

- In this post, we will dive deep into boosting algorithms. The content of this post was extracted from a one-hundred-page paper named [Tree Boosting With XGBoost - Why Does XGBoost Win "Every" Machine Learning Competition?](https://www.semanticscholar.org/paper/Tree-Boosting-With-XGBoost-Why-Does-XGBoost-Win-Nielsen/04e182aa6d36f643a1aea18f3b9384a74538e6a0)

# Supervised Learning

Supervised learning is a part of Machine Learning, which is concerned with **modelling** the relationship between a response variable $Y$ and a set of predictor variables $X$.

There are two kinds of modelling - **explanatory** and **predictive**. In explanatory modelling, we are interested in understanding the causal relationship between $X$ and $Y$, while predictive modelling is concerned with predicting $Y$ using $X$ as predictors.

From now on, we will concern ourself with predictive modelling. In the statistical view, predictive modelling can be viewed as *a problem of function estimation*. The prediction accuracy of the function is measured using a **loss function**, which computes the discrepancy between a prediction and the true outcome.

$$L(y, f(x))$$


(...TO BE CONTINUED)

# References

  Nielsen, D. (2016). Tree Boosting With XGBoost - Why Does XGBoost Win "Every" Machine Learning Competition?