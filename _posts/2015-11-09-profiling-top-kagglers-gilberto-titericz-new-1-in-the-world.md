---
layout: single
title:  "Profiling Top Kagglers: Gilberto Titericz, New #1 in the World"
date:   2015-11-09
permalink: /2015/11/09/profiling-top-kagglers-gilberto-titericz-new-1-in-the-world/
excerpt: ""
categories: 
- Profiling Top Kagglers
tags:
- kaggle
classes: wide
# toc: true
# toc_label: "Table of Contents"
# toc_icon: "cog"
---

Original Post: https://web.archive.org/web/20180628130607/http://blog.kaggle.com/2015/11/09/profiling-top-kagglers-gilberto-titericz-new-1-in-the-world/

---

Kaggle has a new #1 data scientist! Gilberto Titericz usurped Owen Zhang to take the title of #1 Kaggler after his team finished 2nd in the Springleaf Marketing Response competition. As part of our series Profiling Top Kagglers, we interviewed Gilberto to learn more about his background and how he made his way to the top of the Kaggle community.

Gilberto's profile on Kaggle
GILBERTO'S PROFILE ON KAGGLE

Gilberto Titericz Q&A
How did you start with Kaggle competitions?
I am an electronic engineer, but I always had interest in machine learning algorithms. In 2012 I attended the Google AI challenge and when it finished I looked for another way of competing online and found Kaggle via a Google search and I loved it. My first competition was Global Energy Forecasting Competition 2012 - Wind Forecasting and I luckily placed 3rd using a bag of Matlab neural networks. Since then, I've tried to learn more from each competition.

What is your first plan of action when working on a new competition?
First of all it is very important understand the problem, the features, and the evaluation metric. After that I look for a good cross validation strategy. Those are the very basic and essential steps. Only after that you can start thinking about feature engineering and training algorithms that match the problem.

What does your iteration cycle look like?
I always prepare the dataset and apply feature engineering as much as I can, then I choose a training algorithm and optimize hyperparameters based on a cross validation score. If a model is good and stable I save the trainset and testset predictions. Then I start all over again using another training algorithm or model. When I have a handful of good model predictions, I start ensembling at the second level of training.

What are your favorite machine learning algorithms?
Gradient Boosting Machines are the best! It is amazing how GBM can deal with data at a high level of depth. And some details in an algorithm can lead to a very good generalization. GBM is great dealing with linear and non-linear features, also it can handle dense or sparse data. So it's a very good algorithm to understand core parameters and it's always a good choice if you are not sure what algorithm to use. Before I knew of GBM, I was a big fan of neural networks.

What are your favorite machine learning libraries?
I have many favourite libraries, but I will try to rank them according the ones I use most:
- XGBoost - Fast and optimized GBM implementation.
- Vowpal Wabbit - Very fast with lots of parameters and linear algorithms.
- LibFM - Factorization Machines.
- scikit-learn - Lots of functions and algorithms.
- Lasagne - Very good and fast NN implementation (but unfortunately I don't have a GPU).
- Matlab Neural Network Toolbox - Classic.
- R GBM, randomForest and glm - Classic.

What is your approach to hyper-tuning parameters?
I tried grid search in the past, but I found that it consumes a lot of time. So I often use manual brute force searching based on my previous experience. And I always use cross validation to consistently improve the evaluation scores.

What is your approach to solid CV/final submission selection and LB fit?
I always trust my local cross validation score, but in some competitions when the public testset has enough samples and the data is not very noisy I will trust both CV and LB. A good scoring formula I've used before is:

[(LocalCVscore*number_rows_trainset) + (LBscore*number_of_rows_used_to_calculate_LB)] / (sum_of_number_of_rows_in_CV_and_LB )
So for my two final selections I use the formula above if the LB is stable. If not, I usually choose my best reliable Local CV model and the best LB submission model.

In a few words: What wins competitions?
Some good models and features, consistent cross validation methods, teaming up, ensemble meta models, hard work(~15h/week), and always "Luck"!!!

Gilberto's top 8 finishes
GILBERTO'S TOP 8 FINISHES

What is your favourite Kaggle competition and why?
Otto is my favourite. Not only because I won, but in this competition it was possible to apply various methods of machine learning and ensembling techniques. In addition, it was the biggest competition in terms of number of competitors in Kaggle's history.

Final private leaderboard for the Otto Product Classification Challenge
FINAL PRIVATE LEADERBOARD FOR THE OTTO PRODUCT CLASSIFICATION CHALLENGE

What was your least favourite Kaggle competition experience?
Competitions with very small trainset datasets. It makes cross validation and final results unstable. Now I just avoid noisy and small datasets, because it's very hard to apply feature engineering and cross validation efficiently.

What field in machine learning are you most excited about?
Nowadays I'm very interested in deep learning. I think it can still surprise us in the future.

Which machine learning researchers do you study?
Most of what I learn comes from Kaggle competitions, forums, open source code, and scripts.

Can you tell us something about the last algorithm you hand-coded?
I prefer to use open source algorithms and I spend most of my time tuning models. Algorithms I usually hand-code are simple, like feature selection or some kind of training automation.

How important is domain expertise for you when solving data science problems?
It depends on the problem. For example, for the BCI Challenge NER 2015, I'm sure you had to be an expert in the subject to be well placed. The same for the last two CERN competitions (Flavour of Physics & Higgs Boson ML Challenge). If you knew physics, you had a big advantage over others.

But I'm not an expert in the subject matter of all of my winning competitions. Some examples are: Otto Group, Caterpillar, Fast Iron, AMS 2013-2014 Solar Energy Prediction Contest, Springleaf and GEFCom2012. So I believe for most of the problems you can do well even if you aren't an expert.

What do you consider your most creative trick/find/approach?
I don't have that creative trick, but if I can say what I use that gives me more spots it is a second training level ensemble technique. Some people also call that: "stacking models", but it's all the same. That technique depends a lot of correct cross validation and generation of non over fitted meta features. Also it can increase a lot the performance if meta features are generated using different features and training algorithms, because L2 can extract only the best predictions of each meta feature.

Example of stacking models, taken from ML Kaggle Ensembling Guide
EXAMPLE OF STACKING TAKEN FROM THE MLWAVE KAGGLE ENSEMBLING GUIDE

How are you currently using data science at work and does competing on Kaggle help with this?
I work as an automation engineer in a oil refinery. So I don't have much chance to use data science for it. But I can say I'm looking foward to change it on next year. And I can say that most of what I know today about data science I owe it to Kaggle.

What is your opinion on the trade-off between high model complexity and training/test runtime?
That a good question. I confess that I just care about training runtime. Model complexity must be proportional to the CPU power you have and the perfomance that you want. So I always start using simplest dataset as possible and take notes of its training time and performance. After that a good approach in to increase model complexity and note if it increase performance and times. A good tradeoff between complexity and time depends a lot of how much time you have to spend increasing complexity of model and waiting the training time. Usually models that you can build and train in just a few hours are the best, because you will need time to fine tune parameters and it's normal having to train it a lot of time.

What is your view on automating Machine Learning?
Automation is good for preprocess some dataset conditions, cross validation folds, model selection, feature selection and hyperparameters search.
I think all other processes are better if have human interference.

How did you get better at Kaggle competitions?
- Joinning a lot of competitions.
- Learning from Kaggle forums and scripts.
- Trying new algorithms and techniques.
- Teaming up with experienced Kagglers.
- Study competitions code and methods from winners.
- After each competition update your personal helping functions library.
- Dedication. Sometimes when coding I share my laptop screen with my two daughters, they love cartoons.

What did you learn from doing Kaggle competitions?
Kaggle in an excellent place to learn about Data Science. It offers many kind of datasets covering a vast type of problems. I learned a lot after those three years competing and I can say it is addictive. Specially if you are that type of person that like to see the machine learning magic in action.

Bio
I have a MS in Electronic Engineering. In the past 16 years I've been working as an Electronic Engineer for big multinationals like Siemens, Nokia, and later as an Automation Engineer for Petrobras Brasil. In 2008 I started learning Data Science by myself, at first to improve personal stock market gains. In 2012 I joined Kaggle.com and started to continually learn more. See Gilberto's LinkedIn.
