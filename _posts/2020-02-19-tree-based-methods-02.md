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
- bootstrap
- bagging
- random forests
- boosting
- ensemble
- algorithm
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

## The Approach

Decision trees suffer from **high variance**. To reduce the variance, hence increace the test prediction accuracy, we might use a simple but extremely powerful idea - the **bootstrap** method.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-19-tree-based-methods-02/1.png?raw=true">
  <figcaption>Source: blogs.sas.com</figcaption>
</figure>

Recall that given a set of $n$ independent observations $Z_1, ... , Z_n$ each with variance $σ^2$, the variance of the mean $\bar{Z}$ of the observations is given by $σ^2/n$. In other words, **averaging a set of observations reduces variance**. Hence a natural way to reduce the variance and hence increase the prediction accuracy of decision trees is to 

- take many training sets from the population,
- build a separate decision tree using each training set, and
- average the resulting predictions.

Of course, this is not practical because we generally do not have access to multiple training sets. Instead, we can bootstrap, by taking repeated samples from the (single) training data set. In this approach we generate $B$ different bootstrapped training data sets. We then train a decision tree on the $b^{th}$ bootstrapped training set in order to get $\hat{tree_b}(x)$, and finally average all the predictions (for regression trees), to obtain 

$$\frac{1}{B} \sum\limits_{b=1}^B \hat{tree_b}(x)$$

or take the majority vote (for classification trees).

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-19-tree-based-methods-02/0.png?raw=true">
  <figcaption>An illustration of bagging for classification. Source: researchgate.net</figcaption>
</figure>

This is called **Bootstrap aggregation,** or **bagging**.

## Variable Importance Measures

As we have known, bagging typically results in improved accuracy over prediction using a single tree. Unfortunately, it can be difficult to interpret the resulting model after combining hundreds or even thousands of trees.

There is one way to obtain an overall sumarry of the importance of each predictor using the RSS (for regression trees) or the Gini index (for classification trees).

- In the case of bagging regression trees, we can record the total amount that the RSS is decreased due to splits over a given predictor, averaged over all B trees. A large value indicates an important predictor.
- Similarly, in the context of bagging classification trees, we can add up the total amount that the Gini index is decreased by splits over a given predictor, averaged over all B trees.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-19-tree-based-methods-02/2.png?raw=true">
  <figcaption>An example of variable importance plot. Variable importance is computed using the mean decrease in Gini index, and expressed relative to the maximum.</figcaption>
</figure>

# Random Forests

One problem of the bagging approach is that if there is one very strong predictor in the data set, along with a number of other moderately strong predictors. Then in the collection of bagged trees, most or all of the trees will use this strong predictor in the top split. Consequently, all of the trees will *look quite similar to each other*. Hence the predictions from the bagged trees will be **highly correlated** which diminishes the effect in reducing the variance of bootstrap method.

Random forests provide an improvement over bagged trees by way of a random small tweak that **decorrelates** the trees. As in bagging, we build a number of decision trees on bootstrapped training samples. But to overcome the problem, random forests force each split of a tree to **consider only a random sample of $m$ predictors**. Typically, we choose $m = \sqrt{p}$ - that is, the number of predictors considered at each split is approximately equal to the square root of the total number of predictors. We can think of this process as *decorrelating* the trees, thereby making the average of the resulting trees less variable and hence more reliable.

The figure below illustrates the test error when using random forests with different values of m with respect to the number of trees. As we can see, when $m=p$, random forests are just bagging. The choice $m = \sqrt{p}$ gave a small improvement in test error over bagging. The error rate of a single tree was about 45% while it was only 20% to 25% for bagging and random forests.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-19-tree-based-methods-02/3.png?raw=true">
</figure>

# Boosting

Recall that bagging involves creating multiple bootstrapped training data samples from the original training data set and fitting a seperate decision tree to each of the samples, then combining all of the trees to create a single predictive model. Notably, these trees are independent of each other.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-19-tree-based-methods-02/4.png?raw=true">
</figure>

Boosting works in a similar way, except that the trees are grown **sequentially and dependently**: each tree is grown using information from previously grown trees.

Here is how the boosted model is built:

- Build trees one-by-one
- Then the prediction of each tree are summed:

    $$ D_t(x) = \lambda tree_1(x) + \lambda tree_2(x) + ... + \lambda tree_t(x)$$

- The next tree tries to reconstruct the residuals of the target function $f(x)$ and the current ensemble prediction $D_t(x)$:

    $$ tree_t+1(x) \approx f(x) - D_t(x)$$

Unlike fitting the training data set with a single tree which tries to **learn hard** and potentially be overfitted, the boosting approach instead **learns slowly**. The shrinkage parameter $\lambda$ slows the process down even further, allowing more and different shaped trees to attack the residuals.

# References

  James, G., Witten, Daniela, author, Hastie, Trevor, author, & Tibshirani, Robert, author. (2015). An introduction to statistical learning : with applications in R.