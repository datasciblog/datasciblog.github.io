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
classes: wide
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

# Introduction

These are some takeaways from [Activation Functions lecture](https://www.coursera.org/learn/neural-networks-deep-learning/lecture/4dDC1/activation-functions) of Prof. Andrew Ng about choosing activation functions for Neural Networks.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-12-06-DL-01-activation-functions/1.png?raw=true">
	<figcaption>Activation functions and their derivatives</figcaption>
</figure>

# Tanh vs Sigmoid
- In general, **tanh** is almost always superior to **sigmoid** function.
- One exception of using **sigmoid** function is for the output layer of a binary classifier.
- Both functions could slow down gradient descent as their derivatives become very small at two *tails* (*the vanishing gradient problem*).

# ReLU and leaky ReLU
- **ReLU** does not suffer from the vanishing gradient problem as tanh and sigmoid. It is a very common choice these days.
- The disadvantage of **ReLU** is its derivative equals 0 when the input value is negative. This is why we have **leak ReLU**.

