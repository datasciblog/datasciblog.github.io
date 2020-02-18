---
layout: single
title:  "Tree-based-01: The Basics of Decision Trees"
date:   2020-02-18
permalink: /2020/02/18/tree-based-01/
excerpt: ""
categories: 
- Projects
tags:
- tree-based
- decision tree
classes: wide
# toc: true
# toc_label: "Table of Contents"
# toc_icon: "cog"
---

# Introduction

- Tree-based methods are used for both regression and classification problems. The methods are simple and useful for **interpretation**.
- A decision tree is a weak learner compared to other predictive machine learning algorithms. We need other approaches such as **bagging**, **random forests** and **boosting** to improve the prediction accuracy.
- These approaches involve producing a large number of trees which are then combined to yeild a single prediction. This prediction is often dramatically impr  oved in accuracy but also costs some **loss in the interpretability** of the model.

# The Basics of Decision Trees

## Regression Trees

### Example

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/37312e74-1e17-49df-9048-fc1c96ffb7c2/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/37312e74-1e17-49df-9048-fc1c96ffb7c2/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ca17bc9c-939d-40d0-bb62-204eb4efd295/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ca17bc9c-939d-40d0-bb62-204eb4efd295/Untitled.png)

The example shows how to use a decision tree to predict the (log) salary of a baseball player based on **Years** (the number of years that he has played in the major leagues) and **Hits** (the number of hits that he made in the previous year). The tree has two **internal nodes (**The points along the tree where the predictor space is split) and three **terminal nodes (leaves)**. The number in each leaf is the mean of the response for the observations that fall there.

Overall, the tree segments all players into three groups /boxes / leaves: $R1 ={X | Years<4.5}, R2 ={X | Years>=4.5,Hits<117.5}, and R3 ={X | Years>=4.5, Hits>=117.5}$. The predicted salaries for these three groups are $1,000×e^5.107 =$165,174, $1,000×e^5.999 =$402,834, and $1,000×e^6.740 =$845,346 respectively.

We might interpret the regression tree as follows: Years is the most important factor in determining Salary, and players withless experience earn lower salaries than more experienced players. Giventhat a player is less experienced, the number of hits that he made in the previous year seems to play little role in his salary. But among players who have been in the major leagues for five or more years, the number of hitsmade in the previous year does affect salary, and players who made morehits last year tend to have higher salaries. The regression tree shown in Figure 8.1 is likely an over-simplification of the true relationship between Hits, Years, and Salary. However, it has advantages over other types ofregression models: it is easier to interpret, and has a nice graphical representation.

### The process of building a regression tree

Roughly speaking,there are two steps.

1. We divide the predictor space—that is, the set of possible values for X1, X2, . . . , Xp—into J distinct and non-overlapping regions, R1, R2, . . . , RJ.

2. For every observation that falls into the region Rj, we make the sameprediction, which is simply the mean of the response values for thetraining observations in Rj

How do we construct the regions R1, . . . , RJ? In theory, the goal is to find boxes R1, . . . , RJ that minimize the RSS, given by

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0488a1d6-5041-4a85-8720-3658deaac416/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0488a1d6-5041-4a85-8720-3658deaac416/Untitled.png)

Unfortunately, it is computationally infeasible to consider every possible partition of the feature space into J boxes. For this reason, we take a **top-down, greedy** approach that is known as recursive binary splitting. The approach is **top-down** because it begins at the top of the tree (at which pointall observations belong to a single region) and then successively splits thepredictor space; each split is indicated via two new branches further downon the tree. It is **greedy** because at each step of the tree-building process, the best split is made at that particular step, rather than looking ahead and picking a split that will lead to a better tree in some future step.

In order to perform recursive binary splitting, we first select the predictor Xj and the cutpoint s such that splitting the predictor space intothe regions {X|Xj < s} and {X|Xj ≥ s} leads to the greatest possiblereduction in RSS. That is, we consider allpredictors X1, . . . , Xp, and all possible values of the cutpoint s for each ofthe predictors, and then choose the predictor and cutpoint such that theresulting tree has the lowest RSS.

Next, we repeat the process, looking for the best predictor and best cutpoint in order to split the data further so as to **minimize the RSS within each of the resulting regions**. 

The process continues until a stopping criterion is reached; for instance, we may continue until no region containsmore than five observations.

Once the regions R1, . . . , RJ have been created, we predict the response for a given test observation using the mean of the training observations in the region to which that test observation belongs.

A five-region example of this approach is shown in Figure 8.3.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/51d5f902-d69e-4d87-aa5c-994e553f232e/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/51d5f902-d69e-4d87-aa5c-994e553f232e/Untitled.png)

FIGURE 8.3. Top Left: A partition of two-dimensional feature space that could not result from recursive binary splitting. Top Right: The output of recursivebinary splitting on a two-dimensional example. Bottom Left: A tree correspondingto the partition in the top right panel. Bottom Right: A perspective plot of theprediction surface corresponding to that tree.

## Classification Trees

Recall that for a regression tree, the predicted response for an observation is given by the **mean** response of the training observations that belong to the same terminal node. In contrast, for a classification tree, we predict that each observation belongs to the **most commonly occurring class** of training observations in the region to which it belongs.

Just as in the regression setting, we use recursivebinary splitting to grow a classification tree. However, in the classificationsetting, RSS cannot be used as a criterion for making the binary splits. A natural alternative to RSS is the **classification error rate**. Since we plan to assign an observation in a given region to the most commonly occurring class of training observations in that region, the classification error rate issimply the fraction of the training observations in that region that do not belong to the most common class:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e68d5440-a296-43f5-a444-b347252930d2/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e68d5440-a296-43f5-a444-b347252930d2/Untitled.png)

Here ˆ pmk represents the proportion of training observations in the mthregion that are from the kth class. However, it turns out that classification error is not sufficiently sensitive for tree-growing, and in practice two other measures are preferable. 

The Gini index is defined by

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5e8f92d2-a1c0-4a88-ac67-751d850e8697/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5e8f92d2-a1c0-4a88-ac67-751d850e8697/Untitled.png)

a measure of total variance across the K classes. It is not hard to see that the Gini index takes on a small value if all of the ˆ pmk’s are close tozero or one. For this reason the Gini index is referred to as a measure of node **purity**—a small value indicates that a node *contains predominantly observations from a single class*.

An alternative to the Gini index is entropy, given by

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/06269d9c-a520-400e-bb12-581d48845968/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/06269d9c-a520-400e-bb12-581d48845968/Untitled.png)

One can show that the entropy will take on a value near zero if the pˆmk’s are all near zero or near one. Therefore, like the Gini index, the entropy will take on a small value if the mth node is pure. In fact, **it turns out that the Gini index and the entropy are quite similar numerically**.

## Advantages and Disadvantages of Trees

- Very easy to interpret and explain. In fact, they are even easier to explain than linear regression.
- More closely mirror human decision-making than other approaches.
- Easily to handle qualitative predictors
- Unfortunately, they are generally low at predictive accuracy. Trees can also be very **non-robust**. In other words, a small change in the data can lead to a large change in the final tree.
- However, by aggregating many decision trees, using methods like bagging,random forests, and boosting, the predictive performance of trees can besubstantially improved.