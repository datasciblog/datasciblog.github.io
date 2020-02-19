---
layout: single
title:  "Tree-based-02: Bagging, Random Forests and Boosting"
date:   2020-02-19
permalink: /2020/02/19/tree-based-02/
excerpt: ""
categories: 
- Machine Learning
tags:
- tree-based
- decision tree
- bagging
- random forests
- boosting
- ensemble
- algorithms
classes: wide
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

# Introduction

- Decision trees are a weak learner in comparision with other machine learning algorithms.
- However, when trees are used as building blocks of bagging, random forests and boosting methods, we will have very powerful prediction models.
- In fact, **XGBoost** and **LightGBM** - the implementations of gradient boosted decision trees - are the two most popular methods for competitions with structured data in Kaggle.

# Bagging

Decision trees suffer from **high variance**. To reduce the variance, hence increace the test prediction accuracy, we might use a simple but extremely powerful idea - the **bootstrap** method.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-19-tree-based-methods-02/1.png?raw=true">
    <figcaption>Source: blogs.sas.com</figcaption>
</figure>

Recall that given a set of $n$ independent observations $Z_1, ... , Z_n$ each with variance $σ^2$, the variance of the mean $\bar{Z}$ of the observations is given by $σ^2/n$. In other words, **averaging a set of observations reduces variance**. Hence a natural way to reduce the variance and hence increase the prediction accuracy of decision trees is to 

- take many training sets from the population,
- build a separate decision tree using each training set, and
- average the resulting predictions.

Of course, this is not practical because we generally do not have access to multiple training sets. Instead, we can bootstrap, by taking repeated samples from the (single) training data set. In this approach we generate $B$ different bootstrapped training data sets. We then train a decision tree on the $b^{th}$ bootstrapped training set in order to get $\hat{tree}(X_b)$, and finally average all the predictions, to obtain 

$$\frac{1}{B} \sum\limits_{b=1}^B \hat{tree}(X_b).$$

 This is called **Bootstrap aggregation,** or **bagging**.

# References

  James, G., Witten, Daniela, author, Hastie, Trevor, author, & Tibshirani, Robert, author. (2015). An introduction to statistical learning : with applications in R.