---
layout: single
title:  "TreeBoosting-03: Tree Boosting With XGBoost"
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

- In this post, we will dive deep into boosting algorithms. The content of this post was extracted from a one-hundred-page paper named *[Tree Boosting With XGBoost - Why Does XGBoost Win "Every" Machine Learning Competition?](https://www.semanticscholar.org/paper/Tree-Boosting-With-XGBoost-Why-Does-XGBoost-Win-Nielsen/04e182aa6d36f643a1aea18f3b9384a74538e6a0)*

# Supervised Learning

Supervised learning is a part of Machine Learning, which is concerned with **modelling** the relationship between a response variable $Y$ and a set of predictor variables $X$.

There are two kinds of modelling - **explanatory** and **predictive**. In explanatory modelling, we are interested in understanding the causal relationship between $X$ and $Y$, while predictive modelling is concerned with predicting $Y$ using $X$ as predictors.

From now on, we will concern ourself with predictive modelling. In the statistical view, predictive modelling can be viewed as *a problem of function estimation*. The prediction accuracy of the function is measured using a **loss function**, which measures the discrepancy between a prediction and the true outcome.

$$L(y, f(x))$$

While the loss function measures the accuracy of a prediction after the outcome is observed. At the time we make the prediction however, the true outcome is still
unknown, and the loss incurred is consequently a random variable $L(Y, f(X))$. The **true risk** of function $f$ is defined as the *expected loss*

$$R(f) = E[L(Y, f(X))]$$

The **target function** is now defined as 

$$f^{*} = \underset{f}{\arg\min} R(f)$$

and we are going to estimate this target function.

Unfortunately, since we may never know the true risk $R(f)$, we need to rely on the **empirical risk** when inferring our model.

$$\hat{R} = \frac{1}{n} \sum\limits_{i=1}^n L(y_i, f(x_i))$$

By the strong law of large numbers we have that

$$\lim_{x\to\infty} \hat{R}(x) = R(x)$$

almost surely.

The problem of function estimation is now to estimate the **empirical target function**

$$\hat{f} = \underset{f}{\arg\min} \hat{R}(f)$$


**Empirical risk minimization** (ERM) is an induction principle which relies on minimization of the empirical risk. ERM is a criterion to select the optimal function $\hat{f}$ from a set of functions $\mathcal{F}$, also called **model class**. The choice of $\mathcal{F}$ is of major importance.

The perhaps most popular model class is the class of linear models

$$ \mathcal{F} = \{ f : f(x) = \theta_0 + \sum\limits_{j=1}^p \theta_j x_j \} $$


(...TO BE CONTINUED)

# References

  Nielsen, D. (2016). Tree Boosting With XGBoost - Why Does XGBoost Win "Every" Machine Learning Competition?