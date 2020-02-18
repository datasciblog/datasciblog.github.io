---
layout: single
title:  "Tree-based-01: The Basics of Decision Trees"
date:   2020-02-18
permalink: /2020/02/18/tree-based-01/
excerpt: ""
categories: 
- Machine Learning
tags:
- tree-based
- decision tree
- algorithms
classes: wide
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

# Introduction

- Tree-based methods are used for both **regression** and **classification** problems. The methods are simple and useful for **interpretation**.
- A decision tree is a weak learner compared to other predictive machine learning algorithms. We need other approaches such as **bagging**, **random forests** and **boosting** to improve the prediction accuracy.
- These approaches involve producing a large number of trees which are then combined to yeild a single prediction. This prediction is often dramatically improved in accuracy with a cost of some **loss in the interpretability**.

# Regression Trees

## An Example of Regression Trees

<figure class="half">
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-18-tree-based-methods-01/1.png?raw=true">
    <img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-18-tree-based-methods-01/2.png?raw=true">
</figure>

The example shows how to use a decision tree to predict the *log* salary of a baseball player based on *Years* - the number of years that he has played in the major leagues and *Hits* - the number of hits that he made in the previous year. The tree has two **internal nodes** - the points along the tree where the predictor space is split (i.e. $Years < 4.5$ and $Hits < 117.5$) and three **terminal nodes (leaves)**. The number in each leaf is the **mean** of the response for the observations that fall there.

Overall, the tree segments all players into three groups (or leaves): 
- $R_1 = \{ X \| Years<4.5 \}$
- $R_2 = \{ X \| Years>=4.5,Hits<117.5 \}$
- $R_3 = \{ X \| Years>=4.5, Hits>=117.5 \}$

The predicted salaries for these three groups are $1,000 \times e^{5.107} = 165,174$, $1,000 \times e^{5.999} = 402,834$, and $1,000 \times e^{6.740} = 845,346$ respectively.

## The Interpretation of a Regression Tree
We might interpret the regression tree as follows: 
- Years is the most important factor in determining Salary, and players withless experience earn lower salaries than more experienced players. 
- Given that a player is less experienced, the number of hits that he made in the previous year seems to play little role in his salary. But among players who have been in the major leagues for five or more years, the number of hit smade in the previous year does affect salary, and players who made more hits last year tend to have higher salaries. 
- The regression tree shown above is likely an over-simplification of the true relationship between Hits, Years and Salary. However, it has advantages over other types of regression models: **it is easier to interpret, and has a nice graphical representation.**

## The Process of Building a Regression Tree

Roughly speaking, there are two steps:

1. We divide the predictor space - that is, the set of possible values for $X_1, X_2, ... , X_p$ - into $J$ distinct and non-overlapping regions, $R_1, R_2, ... , R_J$.

2. For every observation that falls into the region $R_j$, we make the same prediction, which is simply the mean of the response values for the training observations in $R_j$.

How do we construct the regions $R_1, ... , R_J$? In theory, the goal is to find boxes $R_1, ... , R_J$ that minimize the $RSS$, given by

$$ \sum\limits_{j=1}^J \sum\limits_{i \in R_j} (y_i - \hat{y}_{R_j})^2 , $$

Unfortunately, it is computationally infeasible to consider every possible partition of the feature space into $J$ boxes. For this reason, we take a top-down and greedy approach that is known as **recursive binary splitting**. 
- The approach is **top-down** because it begins at the top of the tree (at which point all observations belong to a single region) and then successively splits the predictor space; each split is indicated via two new branches further down on the tree. 
- It is **greedy** because at each step of the tree-building process, the best split is made at that particular step, rather than looking ahead and picking a split that will lead to a better tree in some future steps.

In order to perform recursive binary splitting:
- We first select the predictor $X_j$ and the cutpoint $s$ such that splitting the predictor space into the regions $ \{ X \| X_j < s \}$ and $ \{ X \| X_j ≥ s \}$ leads to the greatest possible reduction in $RSS$. That is, we consider all predictors $X_1, ... , X_p$, and all possible values of the cutpoint $s$ for each of the predictors, and then choose the predictor and cutpoint such that there sulting tree has the lowest $RSS$.
- Next, we repeat the process, looking for the best predictor and best cutpoint in order to split the data further so as to minimize the $RSS$ within each of the resulting regions. 

The process continues until a stopping criterion is reached; for instance, we may continue until no region contains more than five observations.

Once the regions $R_1, ... , R_J$ have been created, we predict the response for a given test observation using the mean of the training observations in the region to which that test observation belongs.

A five-region example of this approach is shown below.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2020-02-18-tree-based-methods-01/4.png?raw=true">
    <figcaption>Top Left: A partition of two-dimensional feature space that could not result from recursive binary splitting. Top Right: The output of recursivebinary splitting on a two-dimensional example. Bottom Left: A tree correspondingto the partition in the top right panel. Bottom Right: A perspective plot of theprediction surface corresponding to that tree.</figcaption>
</figure>

# Classification Trees

Recall that for a regression tree, the predicted response for an observation is given by the mean response of the training observations that belong to the same terminal node. In contrast, for a classification tree, we predict that each observation belongs to the **most commonly occurring class** of training observations in the region to which it belongs.

Just as in the regression setting, we use recursive binary splitting to grow a classification tree. However, in the classification setting, $RSS$ cannot be used as a criterion for making the binary splits. A natural alternative to $RSS$ is the **classification error rate** - the fraction of the training observations in that region that do not belong to the most common class:

$$ E = 1 - max_k(\hat{p}_{mk}) $$

Here $\hat{p}_{mk}$ represents the proportion of training observations in the $m^{th}$ region that are from the $k^{th}$ class. However, it turns out that classification error is not sufficiently sensitive for tree-growing, and in practice two other measures are preferable. 

The **Gini index** is defined by

$$ G = \sum\limits_{k=1}^K \hat{p}_{mk}(1-\hat{p}_{mk}) ,$$

a measure of total variance across the K classes. It is not hard to see that the Gini index takes on a small value if all of the $\hat{p}_{mk}$’s are close to zero or one. For this reason the Gini index is referred to as a measure of node **purity** - *the value indicates that a node contains predominantly observations from a single class*.

An alternative to the Gini index is **entropy**, given by

$$ D = -\sum\limits_{k=1}^K  \hat{p}_{mk}log(\hat{p}_{mk}) .$$

One can show that the entropy will take on a value near zero if the $\hat{p}_{mk}$’s are all near zero or near one. Therefore, like the Gini index, the entropy will take on a small value if the $m^{th}$ node is pure. **In fact, it turns out that the Gini index and the entropy are quite similar numerically**.

# Advantages and Disadvantages of Trees

- Very easy to **interpret and explain**. In fact, they are even easier to explain than linear regression.
- More closely **mirror human decision-making** than other approaches.
- Easily to handle **qualitative predictors** (categorical features).
- Unfortunately, they are generally low at predictive accuracy. Trees can also be very **non-robust**. In other words, a small change in the data can lead to a large change in the final tree.
- However, by aggregating many decision trees, using methods like **bagging**, **random forests**, and **boosting**, the predictive performance of trees can be substantially improved.

# References

  James, G., Witten, Daniela, author, Hastie, Trevor, author, & Tibshirani, Robert, author. (2015). An introduction to statistical learning : with applications in R.