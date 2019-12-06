---
layout: single
title:  "StatLearning-01: Introduction to Regression Models "
date:   2019-07-04
permalink: /2019/07/04/introduction-to-regression-models/
excerpt: ""
categories: 
- Statistical Learning
tags:
- regression
- linear models
classes: wide
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

# The Optimal Regression Function

Assume that we have a population data set of X and Y as in the figure below. We try to find an optimal function $f(X)$ that can predict the value of Y given a value of X.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-04-introduction-to-regression-models/1.png?raw=true">
</figure>

Note that, for any given value of X, we have several corresponding values of Y while the function $f(X)$ will produce only one value. This leads us to the optimal regression function which is:

$$f(X) = E(Y|X=x)$$

The bad news is we may never find this optimal function since what we have is only a sample of population data. Look at the figure above again, even if we could find it, there is still irreducible error (which captures measurement errors or other discrepancies) in prediction:

$$\epsilon = Y - f(X)$$

Alternatively, we will try to find the best estimation of $f(X)$ which is $\hat{f}(X)$. To do that, we need to minimize the Mean Squared Error function:

$$E[(Y- \hat{f}(X))^2 | X=x] = [f(x) - \hat{f}(X)]^2 + Var(\epsilon)$$

Since $Var(\epsilon)$  is irreducible, we have only one choice of minimizing $[f(x) - \hat{f}(X)]^2$.

# Nearest Neighbor Averaging

In fact, the data we have usually is a small part of population data. That's why we can never find $E[Y \|X=x]$. Relaxing it, we have a way to find the optimal, which is:

$$f(x) = Ave(Y | X  \in N(x))$$

where $N(x)$ is some neighborhood of $X=x$.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-04-introduction-to-regression-models/2.png?raw=true">
</figure>

The nearest neighbor averaging works well when $p \leq 4$ and $N$ is large. Otherwise, it will be lousy caused by the curse of dimensionality - nearest neighbors tend to be far away in high dimensions. In other words, nearest neighbor averaging does not work in the case of a large number of predictors.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-04-introduction-to-regression-models/3.png?raw=true">
</figure>

How to deal with the curse of dimensionality? We have parametric and structured models such as linear models.

# Linear Models

Linear models is an important example of parametric and structured models.

$$f_L(X) = \beta_0 + \beta_1 X_1 + \beta_2 X_2 +... + \beta_p X_p$$

A linear model is specified by $p+1$ parameters $\beta_0, \beta_1,..., \beta_p$. We try to estimate these parameters by fitting the model to training data. Although it is almost never correct, but still a good and interpretable approximation of the true regression function $f(X)$.

We have here is the simulated values (red points) for income from the model:

$$income = f(education, seniority) + \epsilon$$

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-04-introduction-to-regression-models/4.png?raw=true">
	<figcaption>The simulated model $f(X)$ is the blue surface</figcaption>
</figure>

Linear regression model fit to the simulated data:

$$\hat{f}_L(X) = \hat{\beta}_0 + \hat{\beta}_1 \times education + \hat{\beta}_2 \times seniority$$

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-04-introduction-to-regression-models/5.png?raw=true">
	<figcaption>Linear regression model $\hat{f}_L(X)$</figcaption>
</figure>

More flexible regression model $\hat{f}_S(education, seniority)$ fit to the simulated data. Here we use a technique called a thin-plate spline to fit a flexible surface.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-04-introduction-to-regression-models/6.png?raw=true">
	<figcaption>The fitted model using thin-plate spline technique $\hat{f}_S(X)$
</figcaption>
</figure>

As we can see, the linear model is less accurate and flexible but more interpretable compared to the thin-plate spline model. This is called the trade-off between prediction accuracy and model interpretability.

***
**Reference**:

James, G., Witten, Daniela. author, Hastie, Trevor. author, & Tibshirani, Robert. author. (2013). An Introduction to Statistical Learning with Applications in R (1st ed. 2013.).