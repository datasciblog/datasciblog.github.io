---
layout: single
title:  "Profiling Top Kagglers: KazAnova, Currently #2 in the World"
date:   2015-05-07
permalink: /2015/05/07/profiling-top-kagglers-kazanovacurrently-2-in-the-world/
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

Original Post: https://web.archive.org/web/20180620212056/http://blog.kaggle.com/2015/05/07/profiling-top-kagglers-kazanovacurrently-2-in-the-world/

---

There are Kagglers, there are Master Kagglers, and then there are top 10 Kagglers. Who are these people who consistently win Kaggle competitions? In this series we try to find out how they got to the top of the leaderboards.

First up is KazAnova -- Marios Michailidis -- the current number 2 out of nearly 300,000 data scientists. Marios is a PhD student in machine learning at UCL and a senior data scientist at dunnhumby (organizer of the Kaggle competitions 'Shopper Challenge' and 'Product Launch Challenge').

kazanova

Marios Michailidis Q&A
How did you start with Kaggle competitions?
I wanted a new challenge in the field and learn from the Grand Masters.

I was doing software development about machine learning algorithms, which also led to creating a GUI for credit scoring/analytics by the name KazAnova- a nick name I frequently use in Kaggle to keep reminding myself the passion I have for the field and how it started, but I could only go so far by myself.

Kaggle seemed the right place to learn from the experts.

What is your first plan of action when working on a new competition?
First of all to understand the problem and the metric we are tested on- this is key.
To as-soon-as possible create a reliable cross-validation process that best would resemble the leaderboard or the test set in general as this will allow me to explore many different algorithms and approaches, knowing the impact they could yield.
Understand the importance of different algorithmic families, to see when and where to maximize the intensity (is it a linear or non-linear type of problem?)
Try many different approaches/techniques on a the given problem and seize it from all possible angles in terms of algorithms 'selection, hyper parameter optimization, feature engineering, missing values' treatment- I treat all these elements as hyper parameters of the final solution.
What does your iteration cycle look like?
Sacrifice a couple of submissions in the beginning of the contest to understand the importance of the different algorithms -- save energy for last 100 meters.
Do the following process for multiple models
Select a model and do a recursive loop with the following steps:
Transform data (scaling, log(x+1) values, treat missing values, PCA or none)
Optimize hyper parameters of the model
Do feature engineering for that model (as in generate new features)
Do features' selection for that model (as in reducing them)
Redo previous steps as optimum parameters are likely to have changed slightly
Save hold-out predictions to be used later (meta-modelling)
Check consistency of CV scores with leaderboard. If problematic, re-assess cross-validation process and re-do steps
Create partnerships. Ideally you look for people that are likely to have taken different approaches than you have. Historically (in contrast) I was looking for friends; people I can learn from and people I can have fun with - not so much winning.
Find a good way to ensemble
kazanova-analytics
SCREEN FROM THE KAZANOVA ANALYTICS GUI.

 

What are your favorite machine learning algorithms?
I like Gradient Boosting and Tree methods in general:

Scalable
Non-linear and can capture deep interactions
Less prone to outliers
What are your favorite machine learning libraries?
Scikit for forests.
XGBoost for GBM.
LibLinear for linear models.
Weka for all.
Encog for neural nets.
Lasagne for nets, although I learnt it very recently.
RankLib for functions like NDCG.
boostedtree
IMAGE FROM SLIDES 'INTRODUCTION TO BOOSTED TREES' BY TIANQI CHEN (XGBOOST)

 

What is your approach to hyper-tuning parameters?
I do this very manually.

I have only tried once to use something like Gridsearch. I feel I learn more about the algorithms and why they work the way they do by doing this manually. At the same time I feel that "I do something, it's not only the machine!".

After 40+ competitions I've found that I can get to the top 90% of the best hyper parameters with the first try, so the manual approach has paid off!

What is your approach to solid CV/final submission selection and LB fit?
In regards to CV, I try to best resemble what I am being tested on.

In many situations a random split would not work. For example: In the Acquire valued shoppers' challenge we were mainly tested on different products (offers) than these available on the train set. I made my CV to always try to predict 1 offer using the rest of the offers as this could resemble the test leaderboard better than a random split.

About final selection, I normally go for best Leaderboard submission and best CV submission. In the case of a happy collision, I select something as different as possible with respectable CV result just in case I am lucky!

(A prayer to the god of overfitting is my secret 3rd submission)

In a few words: What wins competitions?
Understand the problem well
Discipline ; To have a well-thorough and documented approach that you follow religiously and defines all the modelling process/framework from how you cross-validate, select models, avoids over fitting (which requires a lot of ...discipline).
Allow room to try problem-specific things or new approaches within that framework
The hours you put in
Have access to the right tools
Make key partnerships
Ensembling
What is your favourite Kaggle competition and why?
The Acquire valued shoppers' challenge, not only because I won and it is relevant to what my team does, but I also had the honour to collaborate with Gert Jacobusse.

The final private leaderboard for the Valued Shopper's Challenge
THE FINAL PRIVATE LEADERBOARD FOR THE VALUED SHOPPER'S CHALLENGE

What was your least favourite Kaggle competition experience?
DecMeg, BCI and such channel-wave type of competitions. They have big data and are very domain specific.

I found it hard to even make my CV working properly, plus I did quite bad. Hopefully I will improve.

What field in machine learning are you most excited about?
I like recommender systems if it can be considered a separate field.

There is a broad spectrum of techniques you can use (which are field specific) and to be able to understand what the customer likes is very challenging and rewarding.

Which machine learning researchers do you study?
I study: Steffen Rendle, Leo Breiman, Alexander Karatzoglou, Michael Jahrer & Andreas Töscher, the Machine Learning and Data Mining Group at National Taiwan University, and Jun Wang & Philip Treleaven.

Can you tell us something about the last algorithm you hand-coded?
It was LibFM for Avazu competition as I believed it could work well in that particular problem. I could not make it work as well as LibFFM apparently.

How important is domain expertise for you when solving data science problems?
For some competitions it is really important.

The fact that I am employed in the recommendation science field and the kind of work that we do within my team, has helped me win the Acquire valued Shoppers challenge.

However I think you can go a long way by following standard approaches even if you don't know the field well, which is also the beauty of machine learning and the fact that some algorithms do a significant job for you.

ensembling

What do you consider your most creative trick/find/approach?
I do multiple ensemble meta-stacking if I can use the term.

During the course of my univariate model tuning I save all the models' outputs. Then I make meta-models with the univariate models selections and most of the times I end up with different ensembles of Meta models.

Sometimes I go to third Meta model with Meta models as inputs (Meta-Meta model).

How are you currently using data science at work and does competing on Kaggle help with this?
Classified!

Kaggle does help in optimizing my methods, learning new skills, meet nice people with same passion, be up to date with new tools and generally stay in touch with what's going on in the field.

What is your opinion on the trade-off between high model complexity and training/test runtime?
That is a big discussion in principle.

I guess there is a trade-off, but there needs to be an understanding that better models are not necessarily the most interpretable ones and that a more complex model (that is likely to score better) is not necessarily less stable/more dangerous.

I guess the optimum solution should be somewhere in the middle (e.g. not an ensemble of 100 models nor Naive Bayes)

The best 8 finishes for KazAnova.
THE BEST 8 FINISHES FOR KAZANOVA.

How did you get better at Kaggle competitions?
Did I ?! 😀

I guess what has helped a lot is:

Seeing previous solutions and end-of-competition threads
Participate in Kaggle forums
Learn the tools
Read papers, websites, machine learning tutorials
Optimize processes (use sparse matrices, cut unnecessary steps, write more efficient code)
Save everything I've done and reuse (and improve). E.g. I keep a separate folder for each competition I've completed.
Dedicate time (had to reduce video games)
Collaborate with others
I have found the following resources useful:

This benchmark by Paul Duan in the Amazon competition (my first ever attempt with Python) for a general modelling framework.
From the same competition : Python code to achieve 0.90 AUC with logistic regression from Miroslaw Horbal to create pairwise interactions with cross-validation.
For text analysis, this benchmark from Abhishek: Beating the benchmark in StumbleUpon Evergreen Challenge
XGBoost benchmark in Higgs Boson competition by Bing Xu
Tinrtgu's FTRL Logistic model in Avazu: Beat the benchmark with less than 1MB of memory
Data science Bowl tutorial for image classification: IPython Notebook Tutorial.
H2O (R) deep learning benchmark from Arno Candel in Africa Soil competition
Lasagne and nolearn tutorial for Otto competition (by the admin) :
Andrew Ng's Coursera course in Machine learning
University of Utah Machine learning slides.
Wikipedia and Google
Are partnerships important in achieving good results?
Very.

Sometimes you cannot measure the impact from one competition only as what you learn from the others may be applicable in the future too. I've been very lucky to have made good and fun collaborations so far and I have learnt from all, especially:

From Gert I've learnt model ensembling, feature engineering and Fourier transforms.
Triskelion and Phil Culliton: Vowpal Wabbit
TVS to avoid over-fitting
Bluefool (or Domcastro) 1st derivatives and BART
Mike, Python!
Giulio, competition management and Lasagne.
Bio
marios-michailidis
Marios Michailidis is Senior Data Scientist in dunnhumby and part-time PhD in machine learning at University College London (UCL) with a focus on improving recommender systems. He has worked in both marketing and credit sectors in the UK Market and has led many analytics projects with various themes including: Acquisition, Retention, Uplift, fraud detection, portfolio optimization and more. In his spare time he has created KazAnova, a GUI for credit scoring 100% made in Java.

Marios loves competing on Kaggle and learning new machine learning tricks. He told us he will create something good for the ML community soon...