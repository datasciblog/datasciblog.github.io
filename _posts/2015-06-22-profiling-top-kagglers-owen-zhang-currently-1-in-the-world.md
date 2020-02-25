---
layout: single
title:  "Profiling Top Kagglers: Owen Zhang, Currently #1 in the World"
date:   2015-06-22
permalink: /2015/06/22/profiling-top-kagglers-owen-zhang-currently-1-in-the-world/
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

*As a Machine Learning learner who have learnt a lot by taking part in competitions esspecially those from Kaggle, I always feel much of enjoyment reading sharing from Kaggle Masters on [Kaggle blog](http://blog.kaggle.com). Unfortainately, when the blog was moved to a [new address](https://medium.com/kaggle-blog), most of the posts seemed to be gone. It took me some time to find a website called [The Wayback Machine](https://web.archive.org/) where all the blog posts were captured. I used these captures to recover some of my favorite posts in the old Kaggle blog. I hope you will enjoy and learn from them as well.*{: .notice--notice} 

[Original Post](http://blog.kaggle.com/2015/06/22/profiling-top-kagglers-owen-zhang-currently-1-in-the-world/)

---

Next up in our series on top Kagglers is the #1: [Owen Zhang](https://www.kaggle.com/owenzhang1) (Zhonghua Zhang). Owen comes from an engineering background and currently works as the Chief Product Officer at DataRobot.

## How did you start with Kaggle competitions?

Back in 2011 I had just switched to analytics as a full time job (after several years working in IT), and was eager to improve my skills and to “prove myself”.

So it was fortuitous that Kaggle came along with the [first Allstate competition](https://www.kaggle.com/c/ClaimPredictionChallenge).

Being in the same industry I felt I had some advantage as well. I was lucky and got [2nd place](http://blog.kaggle.com/2012/01/30/owen-zhang-on-placing-2nd-in-the-claim-prediction-challenge/). As a consequence I became a Kaggle addict.

## What is your first plan of action when working on a new competition?

Submit a “reasonable” model as soon as possible -- to validate my understanding of the problem and the data.

## What does your iteration cycle look like?

It depends on the competition and I usually go through a few stages.

At the beginning I focus on data exploration and try some basic approaches so I iterate pretty quickly.

Once the obvious ideas are exhausted I usually slow down and do some research into the domain -- reading papers, forum post, etc. If I get an idea I would then implement it and submit it to the public LB.

My iteration cycle usually is short -- I rarely work on feature engineering that requires more than a few hours of coding for a particular feature.

My personal experience is that very complicated features usually do not work well -- possibly because of my buggy code.

*[Tips on Modeling Competitions on Kaggle](http://nycdatascience.com/news/featured-talk-1-kaggle-data-scientist-owen-zhang/) (2015) Owen Zhang, NYC Data Science Academy*

## What are your favorite machine learning algorithms?

Again it depends on the problem, but if I have to pick one, then it is GBM (its [XGBoost](https://github.com/dmlc/xgboost) flavor). It is amazing how well it works in many different problems.

Also I am a big fan of online SGD, [factorization](http://libfm.org/), neural networks, each for particular types of problems.

## What are your favorite machine learning libraries?

I used to be a very focus R user until about 1 year ago. But now I am more of a Python user who use whichever library that’s needed, including [scikit-learn](http://scikit-learn.org/stable/), XGBoost, VW, [cuda-convnet2](https://code.google.com/p/cuda-convnet2/) and others.

## What is your approach to hyper-tuning parameters?

I mostly tune by hand -- starting with reasonable values and doing trial and error based [hill climbing](https://en.wikipedia.org/wiki/Hill_climbing). This fits my style -- I like to tinker with the problem in an ad-hoc fashion.

Sometimes I think I should eventually be more disciplined and systematic, using some [Bayesian optimizer](https://en.wikipedia.org/wiki/Bayesian_optimization). However that would take some fun away from the process, I think.

## What is your approach to solid CV/final submission selection and LB fit?

This really depends on if there is a public LB [data leak](https://www.kaggle.com/wiki/Leakage).

For time-sensitive models, it is very common that the public LB gives us “hints” about the private LB. In that case I use almost exclusively the public LB results as validation. If that is the case, I would usually give public LB more weight.

In the case the data is small/noise, I use a combination of CV and public LB.

I also usually choose 2 different models as final results -- one favors public LB and one favors CV.

## In a few words: What wins competitions?

Luck + hard work + experience

## What is your favourite Kaggle competition and why?

Every competition is different and it is hard to pick a single favorite, so I will pick a few:

- The [Amazon access challenge](https://www.kaggle.com/c/amazon-employee-access-challenge) was good because
    1. I got good result (2nd place),
    2. almost all the different things I tried in the competition worked,
    3. I did better than many of my long time nemeses, such as [Leustagos](https://www.kaggle.com/leustagos) and [Gxav](https://www.kaggle.com/xavierconort) (Xavier Conort).
- The [Dogs vs. Cats](https://www.kaggle.com/c/dogs-vs-cats) was very interesting because the problem was interesting. Also this is the first time I actually started learning CNN and it was really fascinating.
- The recent [Otto competition](https://www.kaggle.com/c/otto-group-product-classification-challenge) -- I did quite badly and it is not because of data noise. From methodology perspective I think I learned a lot from others in this one.
What was your least favourite Kaggle competition experience?
Usually I avoid competitions with too little data or too much noise. It is just a lottery.

For example one recent competition had only 130 data points in training, so the results are just random. I don’t participate in those so it is not “experience” per se, but they do make the overall Kaggle experience less perfect than it should be.

## What field in machine learning are you most excited about?

Deep learning is really popular and I am very excited about it, like everyone else.

However I would be really excited if there is a “feature engineering” field. So far it is still mostly ad hoc.

## Which machine learning researchers do you study?

I learned quite a bit by reading the book *[Elements of Statistical Learning](http://statweb.stanford.edu/~tibs/ElemStatLearn/)*, and I also dabble in all the deep learning publications.

However I learned most from my fellow [Kagglers](https://www.kaggle.com/users).

## Can you tell us something about the last algorithm you hand-coded?

I usually use other people’s code. The last “algorithm” I wrote was just generalized linear models with elastic net penalty.

What I found is that it is usually not “efficient” (from time budget) perspective to write my own algorithm for a competition.

Almost always I can find open source code for what I want to do, and my time is much better spent doing research and feature engineering.


[Open Source Tools and Data Science Competitions](http://www.opendatascience.com/blog/videos/owen-zhang-talk-odsc-boston-2015/) (Owen Zhang) - 2015 Boston ODSC

## How important is domain expertise for you when solving data science problems?

It is quite important because often that is an important source of feature engineering. In addition it is not easy or efficient to re-invent the wheels.

The domain can be very broad. For example, I worked in insurance companies, which make me comfortable with not only insurance problems, but business oriented problems in general. On the other hand I can see physicists doing better with more mathematical or scientific problems.

Also it is worth noting that domain expertise has different meaning in different context. To a degree, knowing “overfitting is bad” is also domain expertise.

## What do you consider your most creative trick/find/approach?

I don’t think anything I do is particularly “creative”.

If I have to name one, in the [Allstate purchase option competition](https://www.kaggle.com/c/allstate-purchase-prediction-challenge) (with 7 correlated target variables), I built sequential conditional models, from the most “independent” target to the least “independent” target. However I am pretty sure I was reinventing the wheel.

## How are you currently using data science at work and does competing on Kaggle help with this?

Our company DataRobot’s product is built to help data scientists build generalizable models, and what I learned from Kaggle is very helpful.

For example, if I find a particular approach is effective in certain modeling context, I would make a suggestions to the team to implement that as a feature in our product.

## What is your opinion on the trade-off between high model complexity and training/test runtime?

I assume this is about the trade-off between complexity vs prediction performance. In Kaggle competitions there is no trade-off, we only care about accuracy.

However in reality we rarely implement the most complicated model, for at least 2 reasons:

1. It takes too much effort to train/execute.
2. More complicated models tend to be more brittle.

On the other hand, even if we don’t implement the best performing/most complicated model, such a model still has inherent value:

1. It can provide a benchmark to evaluate simplified models against,
2. It gives us insights that will help us make simplified models better,
3. It helps us detect potential data problems.

## What is your view on automating Machine Learning?

We are in this business so certainly I believe it is doable (and valuable) to a degree.

The mechanical part of machine learning (like CV, hyper parameter tuning, model algorithm selection) will be almost completely automated, so that data scientists can focus on problem selection, model definition, and feature engineering.

## How did you get better at Kaggle competitions?

To be honest I don’t know for sure. I am not even sure that I “got better” or even that I “am good”.

I was definitely lucky. Learning from others on Kaggle certainly improves my skills over time, but the same is true for everyone.

## What did you learn from doing Kaggle competitions?

Too many things to list, but here are a few that come to mind:

- Nothing is certain until the private leaderboard is revealed.
- There are always more things that I don’t know than I do.
- Relying on the public LB is dangerous.
- There is usually a simple elegant approach that does equally well.

## Bio

Owen Zhang currently works as a data scientist at DataRobot a Boston based startup company. His education background is in engineering, with a master’s degree from U of Toronto, Canada, and bachelor’s from U of Science and Technology of China. Before joining DataRobot, he spent more a decade in several U.S. based property and casualty insurance companies, last one being AIG in New York.