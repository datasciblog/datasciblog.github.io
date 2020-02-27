---
layout: single
title:  "TreeBoosting-03: Tree Boosting With XGBoost"
date:   2020-02-26
permalink: /2020/02/26/tree-boosting-03/
excerpt: ""
categories: 
- Machine Learning
tags:
- tree boosting
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

- In this part of the [Tree Boosting series](https://datasciblog.github.io/tags/#tree-boosting), we have already talked about the basics of decision trees which are used as base leaners of tree boosting algorithms. We also discuss several approaches of building ensembling models from decision trees such as bagging, random forests and boosting.

- In this post, we will dive deep into boosting algorithms. The content of this post was extracted from a one-hundred-page paper named *[Tree Boosting With XGBoost - Why Does XGBoost Win "Every" Machine Learning Competition?](https://www.semanticscholar.org/paper/Tree-Boosting-With-XGBoost-Why-Does-XGBoost-Win-Nielsen/04e182aa6d36f643a1aea18f3b9384a74538e6a0)*

# Supervised Learning

Supervised learning is a part of Machine Learning, which is concerned with **modelling** the relationship between a response variable $Y$ and a set of predictor variables $X$.

## Predictive Modelling

There are two kinds of modelling - **explanatory** and **predictive**. In explanatory modelling, we are interested in understanding the causal relationship between $X$ and $Y$, while predictive modelling is concerned with predicting $Y$ by using $X$ as predictors. From now on, we will concern ourself with predictive modelling.

## The Loss Function

 In the statistical view, predictive modelling can be viewed as *a problem of function estimation*. The prediction accuracy of the function is measured using a **loss function**, which measures the discrepancy between a prediction and the true outcome.

$$L(y, f(x))$$

In theory we can use any loss function that reflect discrepancy between the observations and the predictions. In practice however, there are a few popular loss functions which tend to be used for a wide variety of problems. Many of the loss functions used in practice are **likelihood-based**, i.e. negative log-likelihoods.

### Likelihood-based Loss Functions

For **regression**, we assume a conditional Gaussian distribution

$$[Y | X] \sim Normal(\mu(X), \sigma^2).$$

The loss function based on this likelihood is

$$L(y, \mu(x)) = \frac{1}{2} log 2\pi\sigma^2 + \frac{1}{2\sigma^2} (y − \mu(x))^2.$$

Maximum likelihood estimation with a Gaussian error assumption is however equivalent to least-squares regression as the loss function is equivalent to the squared error loss

$$L(y, f(x)) = (y − f(x))^2.$$

For **binary classification**, the Bernoulli distribution is useful. Letting $ \mathcal{Y} = \\{ 0, 1 \\} $, we can assume

$$[Y |X] \sim Bernoulli(p(X)).$$

The loss function based on this likelihood is

$$L(y, p(x)) = −y log(p(x)) − (1 − y) log(1 − p(x))$$

where 

$$p(x) = Prob[Y = 1|X = x].$$

The loss function based on the Bernoulli likelihood is also referred to as the **log-loss**, the **cross-entropy** or the Kullback-Leibler information.

## The Risk Function

While the loss function measures the accuracy of a prediction after the outcome is observed. At the time we make the prediction however, the true outcome is still
unknown, and the loss incurred is consequently a random variable $L(Y, f(X))$. The **true risk** of function $f$ is defined as the *expected loss*

$$R(f) = E[L(Y, f(X))]$$

The **target function** is now defined as 

$$f^{*} = \underset{f}{\arg\min} R(f)$$

and the goal is to estimate this target function.

## Empirical Risk Minimization

Unfortunately, since we may never know the true risk $R(f)$, we need to rely on the **empirical risk** when inferring our model.

$$\hat{R} = \frac{1}{n} \sum\limits_{i=1}^n L(y_i, f(x_i))$$

By the strong law of large numbers we have that

$$\lim_{x\to\infty} \hat{R}(x) = R(x),$$

almost surely.

The problem of function estimation is now to estimate the **empirical target function**

$$\hat{f} = \underset{f\in\mathcal{F}}{\arg\min} \hat{R}(f).$$


**Empirical risk minimization** (ERM) is an induction principle which relies on minimization of the empirical risk. ERM is a criterion to select the optimal function $\hat{f}$ from a set of functions $\mathcal{F}$, so called **model class**. The choice of $\mathcal{F}$ is of major importance.

The perhaps most popular model class is the class of linear models

$$ \mathcal{F} = \{ f : f(x) = \theta_0 + \sum\limits_{j=1}^p \theta_j x_j \} .$$


## The Learning Algorithm

The model class together with the ERM principle reduces the *learning problem* to an *optimization problem*. The computational aspect of the problem is to actually solve the
the optimization problem defined by ERM. This is the job of the *learning algorithm*, which is essentially just an *optimization algorithm*. 

The learning algorithm takes a data set $\mathcal{D}$ as input and outputs a fitted model $\hat{f}$. Most of model classes will have some parameters $\theta$ that the learning algorithm will adjust to fit the data. In this case, model estimation becomes estimating the parameters $\theta$.

$$\hat{f}(x) = f(x;\theta)$$

Common learning methods include

- The Constant
- Linear Methods
- Local Regression Methods
- Basis Function Expansions
- Adaptive Basis Function Models

## The Optimization Algorithm

Different choices of model classes and loss functions will lead to different optimization problems varying in dificulty and thus requiring different approaches. The simplest problems yield analytic solutions. Most problems do however require *numerical methods*.

When the objective function is continuous with respect to $\theta$ we get a **continuous optimization problem**. When this is not the case, we have a **discrete optimization problem**. The continuous optimization problems are typically easier to solve than discrete optimization problems thus are more desirable when it comes to choose the model class and loss function.

One notable example of a model class which leads to a discrete optimization problem is tree models. Most model classes does however lead to continuous optimization problems. There are numerous methods for continuous optimization problems. Two prominent methods that will be important for tree boosting implementation however, is the method of **gradient descent** and **Newton’s method**. **Gradient boosting** and **Newton boosting** are approximate *nonparametric* versions of these optimization algorithms.

### Numerical Optimization in Parameter Space

Assume that we are trying to fit a model $f(x) = f(x;\theta)$ parameterized by $\theta$ then the risk of the model can be written as

$$R(\theta) = E[L(Y,f(X;\theta))]$$

Given that $R(\theta)$ is differentiable with respect to $\theta$ we can estimate $\theta$ using a numerical optimization algorithm such as **gradient descent** or **Newton’s method**.

For both algorithms, at iteration $m$, the estimate of $\theta$ is updated according to

$$\theta^{(m)} = \theta^{(m-1)} + \theta_m$$

where $\theta_m$ is the step taken at iteration $m$.

The resulting estimate of $\theta$ after $M$ iterations can be written as a sum

$$\theta \equiv \theta^{(M)} = \sum\limits_{m=0}^M \theta_m,$$

where $\theta_0$ is an initial guess and $\theta_1$, ..., $\theta_M$ are the successive steps taken by the optimization algorithm.

The difference between two algorithms is in the step $\theta_m$ they take.

#### Gradient Descent

At each interation, gradient descent takes a step along the **direction** of steepest descent of the risk given by

$$−g_m = −\nabla_\theta R(\theta)|_{\theta=\theta^{(m−1)}}.$$

To surely reduce risk however, the length of the step taken should be not too long. A popular way to determine the step length $\rho_m$ to take in the steepest descent direction is to use *line search*

$$\rho_m = \underset{\rho}{\arg\min} R(\theta^{(m-1)} - \rho g_m).$$

The step taken at iteration $m$ can thus be written

$$\theta_m = −\rho_m g_m.$$

#### Newton’s Method

Unlike gradient descent, Newton’s method determines both the step direction and step length at the same time. Newton’s method can be motivated as a way to approximately solve

$$\nabla_{\theta_m} R(\theta^{(m−1)} + \theta_m) = 0$$

By doing a second-order Taylor expansion, we get

$$\nabla_{\theta_m} R(\theta^{(m−1)} + \theta_m) \approx g_m + H_m \theta_m = 0$$

where $H_m$ is the Hessian matrix at the current estimate

$$H_m = \nabla_{\theta}^2 R(\theta)|_{\theta=\theta^{(m−1)}}.$$

The solution to this is given by

$$\theta_m = −H_m^{−1} g_m.$$

From the discussion above, we can see that Newton’s method is a second-order method, while gradient descent is a first-order method.

# Boosting

Boosting refers to a class of learning algorithms that fit the data by combining multiple simple models. Each simple model is learnt using a *base learner* or *weak learner* which tend to have a limited predictive ability, but when selected carefully
using a boosting algorithm, they form a relatively more accurate model. This is the meaning of "boosting".

The early work on boosting focused on binary classification. After that, the view of boosting algorithms as numerical optimization techniques was developed. This led to the development of general boosting algorithms, e.g. **gradient boosting**, that allowed for optimization of any differentiable loss function. Boosting became applicable to general regression problems and not only classification.

## Numerical Optimization in Function Space

Above, we have discussed numerical optimization in parameter space. We will now discuss numerical optimization in function space.

Note that minimizing

$$R(f) = E[L(Y, f(X))]$$

is equivalent to minimizing

$$R(f(x)) = E[L(Y, f(x))|X = x]$$

At a current estimate $f^{(m−1)}$, the "step" $f_m$ is taken in function space to obtain $f^{(m)}$. Analogously to parameter optimization update we can write the update at iteration $m$ as

$$f^{(m)}(x) = f^{(m−1)}(x) + f_m(x)$$

The resulting estimate of $f$ after $M$ iterations can be written as a sum

$$f(x) \equiv f^{(M)}(x) = \sum\limits_{m=0}^M f_m (x),$$

where $f_0$ is an initial guess and $f_1$,..., $f_M$ are the successive "steps" taken in function space.

### Gradient Descent in Function Space

Similar to the case of [gradient descent in parameter space](#gradient-descent), we have the direction of steepest descent of the risk by taking the negative gradient

$$−g_m(x) = − E \left[ \frac{\partial L(Y,f(x))}{\partial f(x)} | X=x \right]_{f(x)=f^{(m−1)}(x)}$$

The step length $\rho_m$ to take in the steepest descent direction can be determined using line search

$$\rho_m = \underset{\rho}{\arg\min} E[L(Y, f^{(m−1)}(X) − \rho g_m(X)].$$

The "step" taken at each iteration $m$ is then given by 

$$f_m(x) = −\rho_m g_m(x).$$

Performing updates iteratively according to this yields the gradient descent algorithm in function space.

### Newton’s Method in Function Space

The Newton "step" in function space is given by

$$f_m (x) = − \frac{g_m(x)}{h_m(x)}$$

where $h_m(x)$ is the Hessian at the current estimate

$$h_m(x) = E \left[ \frac{\partial^2 L(Y,f(x))}{\partial f(x)^2} | X=x \right]_{f(x)=f^{(m−1)}(x)}.$$

## Boosting Algorithms

As seen from the previous sections, boosting fits ensemble models of the kind

$$f(x) =  \sum\limits_{m=1}^M f_m(x).$$

These can be rewritten as adaptive basis function models

$$f(x) = \theta_0 + \sum\limits_{m=1}^M \theta_m \phi_m(x),$$

where $f_0(x) = \theta_0$ and $f_m(x) = \theta_m \phi_m(x)$ for $m = 1, ...M$.

Most boosting algorithms can be seen to solve

$$ \{ \hat{\theta}_m, \hat{\phi}_m \} = \underset{ \{ \theta_m, \phi_m \} }{\arg\min} \sum\limits_{i=1}^n L(y_i, \hat{f}^{(m−1)}(_xi) + \theta_m \phi_m(x_i))$$

either exactly or approximately at each iteration. **Gradient boosting** and **Newton boosting** can be viewed as general algorithms that solve the equation approximately for any suitable loss function. Also, gradient boosting and Newton boosting can be viewed as *empirical versions* of the numerical optimization algorithms in function space we developed above.

### Gradient Boosting

The development of gradient boosting is based on [gradient descent in function space](#gradient-descent-in-function-space) that we derived before. Here, the empirical risk will take the place of the true risk.

### Newton Boosting



## AdaBoost

 AdaBoost is regarded as the first practical boosting algorithm for binary classification. This algorithm fits a weak learner to *weighted* versions of the data *iteratively*. At each iteration, the weights are updated such that the misclassified data points recieve higher weights.

The resulting model can be written

$$\hat{f}(x) \equiv \hat{f}^{(M)}(x) = \sum\limits_{m=1}^M \hat{\theta}_m \hat{c}_m(x)$$

where $\hat{c}_m(x) \in \\{ −1, 1 \\} $ are the weak classifiers and hard classifications are given by $\hat{c}_m(x) = sign(\hat{f}(x))$.

In the statistical view of the algorithm, it has been shown
that AdaBoost was actually minimizing the **exponential loss function**

$$L(y,f(x)) = e^{−yf(x)}.$$



(...TO BE CONTINUED)

# References

  Nielsen, D. (2016). Tree Boosting With XGBoost - Why Does XGBoost Win "Every" Machine Learning Competition?