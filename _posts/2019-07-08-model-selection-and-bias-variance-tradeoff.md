---
layout: single
title:  "StatLearning-02: Model Selection and Bias-Variance Tradeoff"
date:   2019-07-08
permalink: /2019/07/08/model-selection-and-bias-variance-tradeoff/
categories: 
- Statistical Learning
tags:
- Model Selection
- Bias-Variance Tradeoff
classes: wide
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

# Assessing Model Accuracy

For regression problems, we can use mean squared error to assess the accuracy of a model which is:

$$MSE = Ave[y_i - \hat{f}(x_i)]$$

While the $MSE_{Tr}$ on training data may be biased toward overfit models, we should use $MSE_{Te}$ on fresh test data in order to see how well the model performs.

$$MSE_{Te} = Ave_{i \in Te}[y_i - \hat{f}(x_i)]$$

These are some examples of the relationship between the flexibility of a model and its $MSEs$ on training and test data.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-08-model-selection-and-bias-variance-tradeoff/1.png?raw=true">
	<figcaption>Left: Data simulated from f, shown in black. Three estimates off are shown: the linear regression line (orange curve), and two smoothing spline fits (blue and green curves). Right: Training MSE (grey curve), test MSE (red curve), and minimum possible test MSE over all methods (dashed line). Squares represent the training and test MSEs for the three fits shown in the left-hand panel.</figcaption>
</figure>

In this figure above, the dashed line refers to the irreducible error $Var(\epsilon)$ from this formula:

$$E[(Y- \hat{f}(X))^2 | X=x] = [f(x) - \hat{f}(X)]^2 + Var(\epsilon)$$

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-08-model-selection-and-bias-variance-tradeoff/2.png?raw=true">
	<figcaption>Using a different true f that is much closer to linear. In this setting, linear regression provides a very good fit to the data.</figcaption>
</figure>

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-08-model-selection-and-bias-variance-tradeoff/3.png?raw=true">
	<figcaption>Using a different f that is far from linear. In this setting, linear regression provides a very poor fit to the data.</figcaption>
</figure>

# Bias-Variance Tradeoff

Suppose we have a model $\hat{f}(X)$ fitted to training data that drawn from the true model $Y = f(X) + \epsilon$ with $f(x) = E(Y \|X=x)$. Given a test observation $(x_0, y_0)$ from the population, we have a decomposition:

$$E[y_0 - \hat{f}(x_0)]^2 = Var(\hat{f}(x_0)) + Bias(\hat{f}(x_0))^2 + Var(\epsilon)$$

Note that, $Bias(\hat{f}(x_0)) = E[\hat{f}(x_0)] - f(x_0)$. This means that the bias of a model at the point $x_0 $ is the difference between the expected value of $\hat{f}(x_0)$ and the true value $f(x_0)$.

But what is the expected value of $\hat{f}(x_0)$? Remember that, for different training data set, we can have different estimated $\hat{f}(x)$ giving different values for $\hat{f}(x_0)$. The expected value is calculated over all these possible predictions.

Typically as the flexibility of $\hat{f}$ increases, the expected value $E[\hat{f}(x_0)]$ is changing toward the true value $f(x_0)$ making the bias decreased. At the same time, the variability of $\hat{f}(x_0)$ will increase. The bias-variance tradeoff when choosing the flexibility of a model is demonstrated in the figure below.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-07-08-model-selection-and-bias-variance-tradeoff/4.png?raw=true">
</figure>

In short, as the flexibility of a model increases, the variance increases, the bias decreases, and the MSE is always U-curved.

### Reference

James, G., Witten, Daniela. author, Hastie, Trevor. author, & Tibshirani, Robert. author. (2013). An Introduction to Statistical Learning with Applications in R (1st ed. 2013.).
