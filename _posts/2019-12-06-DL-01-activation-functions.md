---
layout: single
title:  "DL-01: Choosing Activation Functions for Neural Networks "
date:   2019-12-06
permalink: /2019/12/06/choosing-activation-functions-for-neural-networks/
excerpt: ""
categories: 
- Deep Learning
tags:
- activation function
- deep learning specialisation
- coursera
- gradient descent
classes: wide
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

# Introduction

These are some takeaways from [Activation Functions lecture](https://www.coursera.org/learn/neural-networks-deep-learning/lecture/4dDC1/activation-functions) of Prof. Andrew Ng about choosing activation functions for Neural Networks.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-12-06-DL-01-activation-functions/1.png?raw=true">
	<figcaption>Activation functions in comparison. Red curves stand for, respectively, sigmoid, hyperbolic tangent, ReLU, and Softplus functions. Their first derivative is plotted in blue. (Source: researchgate.net)</figcaption>
</figure>

# Tanh vs Sigmoid
- Most of the time, **tanh** is superior to **sigmoid** function.
- One exception of using **sigmoid** function is for the output layer of a binary classifier.
- However, both functions could slow down the gradient descent algorithm as their derivatives become very small when input values are very large which usually occurs in training neural networks (*the vanishing gradient problem*).

# ReLU vs leaky ReLU
- **ReLU** does not suffer from the vanishing gradient problem. It is a very common choice these days.
- A disadvantage of **ReLU** is that its derivative is equal to 0 for negative input values. This is why we have **leak ReLU**. However, **leak ReLU** is not used as much as **ReLU** in practice. This is because when training neural networks, the input of ReLU function is usually large which can help overcome the disadvantage.