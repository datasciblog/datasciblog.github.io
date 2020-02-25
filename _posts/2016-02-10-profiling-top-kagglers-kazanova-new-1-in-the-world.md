---
layout: single
title:  "Profiling Top Kagglers: KazAnova, New #1 in the World"
date:   2016-02-10
permalink: /2016/02/10/profiling-top-kagglers-kazanova-new-1-in-the-world/
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

<div class="notice--info">
As a Machine Learning learner who have learnt a lot by taking part in competitions esspecially those from Kaggle, I always feel much of enjoyment reading sharing from Kaggle Masters on <a href="http://blog.kaggle.com">Kaggle blog</a>. Unfortainately, when the blog was moved to a <a href="https://medium.com/kaggle-blog">new address</a>, most of the posts seemed to be gone. It took me some time to find a website called <a href="https://web.archive.org/">The Wayback Machine</a> where all the blog posts were captured. I used these captures to recover some of my favorite posts in the old Kaggle blog. I hope you will enjoy and learn from them as well.
</div>

---

*This blog was originally published on May 7, 2015 when Marios Michailidis was ranked #2. Marios is now the number 1 data scientist out of 465,000 data scientists! We wanted to re-share the original post, with a few additions and updates from Marios.*

---
 
There are Kagglers, there are Master Kagglers, and then there are top 10 Kagglers. Who are these people who consistently win Kaggle competitions? In this series we try to find out how they got to the top of the leaderboards.

First up is [KazAnova](https://www.kaggle.com/users/111640/kazanova) -- Marios Michailidis -- the current number 2 (now #1) out of nearly 300,000 (now 465,000+) data scientists. Marios is a PhD student in machine learning at [UCL](http://www.cs.ucl.ac.uk/) and a Manager of Data Science at [dunnhumby](http://www.dunnhumby.com/) (organizer of the Kaggle competitions '[Shopper Challenge](https://www.kaggle.com/c/dunnhumbychallenge' and '[Product Launch Challenge](https://www.kaggle.com/c/hack-reduce-dunnhumby-hackathon').

## How did you start with Kaggle competitions?

I wanted a new challenge in the field and learn from the Grand Masters.

I was doing software development about machine learning algorithms, which also led to creating a GUI for credit scoring/analytics by the name KazAnova- a nick name I frequently use in Kaggle to keep reminding myself the passion I have for the field and how it started, but I could only go so far by myself.

Kaggle seemed the right place to learn from the experts.

## What is your first plan of action when working on a new competition?

1. First of all to understand the problem and the metric we are tested on- this is key.
2. To as-soon-as possible create a reliable cross-validation process that best would resemble the leaderboard or the test set in general as this will allow me to explore many different algorithms and approaches, knowing the impact they could yield.
3. Understand the importance of different algorithmic families, to see when and where to maximize the intensity (is it a linear or non-linear type of problem?)
4. Try many different approaches/techniques on a the given problem and seize it from all possible angles in terms of algorithms 'selection, hyper parameter optimization, feature engineering, missing values' treatment- I treat all these elements as hyper parameters of the final solution.

## What does your iteration cycle look like?

1. Sacrifice a couple of submissions in the beginning of the contest to understand the importance of the different algorithms -- save energy for last 100 meters.
2. Do the following process for multiple models
- Select a model and do a recursive loop with the following steps:
    - Transform data (scaling, log(x+1) values, treat missing values, PCA or none)
    - Optimize hyper parameters of the model
    - Do feature engineering for that model (as in generate new features)
    - Do features' selection for that model (as in reducing them)
    - Redo previous steps as optimum parameters are likely to have changed slightly
- Save hold-out predictions to be used later (meta-modelling)
- Check consistency of CV scores with leaderboard. If problematic, re-assess cross-validation process and re-do steps
3. Create partnerships. Ideally you look for people that are likely to have taken different approaches than you have. Historically (in contrast) I was looking for friends; people I can learn from and people I can have fun with - not so much winning.
4. Find a good way to ensemble

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2016-02-10-profiling-top-kagglers-kazanova-new-1-in-the-world/1.png?raw=true">
  <figcaption>SCREEN FROM THE KAZANOVA ANALYTICS GUI.</figcaption>
</figure>

## What are your favorite machine learning algorithms?

I like Gradient Boosting and Tree methods in general:
1. Scalable
2. Non-linear and can capture deep interactions
3. Less prone to outliers

## What are your favorite machine learning libraries?

1. Scikit for forests.
2. XGBoost for GBM.
3. LibLinear for linear models.
4. Weka for all.
5. Encog for neural nets.
6. Lasagne for nets, although I learnt it very recently.
7. RankLib for functions like NDCG.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2016-02-10-profiling-top-kagglers-kazanova-new-1-in-the-world/2.png?raw=true">
  <figcaption>IMAGE FROM SLIDES 'INTRODUCTION TO BOOSTED TREES' BY TIANQI CHEN (XGBOOST)</figcaption>
</figure>

## What is your approach to hyper-tuning parameters?

I do this very manually.

I have only tried once to use something like Gridsearch. I feel I learn more about the algorithms and why they work the way they do by doing this manually. At the same time I feel that "I do something, it's not only the machine!".

After 60+ competitions I've found that I can get to the top 90% of the best hyper parameters with the first try, so the manual approach has paid off!

## What is your approach to solid CV/final submission selection and LB fit?

In regards to CV, I try to best resemble what I am being tested on.

In many situations a random split would not work. For example: In the Acquire valued shoppers' challenge we were mainly tested on different products (offers) than these available on the train set. I made my CV to always try to predict 1 offer using the rest of the offers as this could resemble the test leaderboard better than a random split.

About final selection, I normally go for best Leaderboard submission and best CV submission. In the case of a happy collision, I select something as different as possible with respectable CV result just in case I am lucky!

(A prayer to the god of overfitting is my secret 3rd submission)

## In a few words: What wins competitions?

1. Understand the problem well
2. Discipline ; To have a well-thorough and documented approach that you follow religiously and defines all the modelling process/framework from how you cross-validate, select models, avoids over fitting (which requires a lot of ...discipline).
3. Allow room to try problem-specific things or new approaches within that framework
4. The hours you put in
5. Have access to the right tools
6. Make key partnerships
7. Ensembling

## What is your favourite Kaggle competition and why?

The [Acquire valued shoppers](https://www.kaggle.com/c/acquire-valued-shoppers-challenge)' challenge, not only because I won and it is relevant to what my team does, but I also had the honour to collaborate with [Gert Jacobusse](http://www.kaggle.com/users/9974/gert).

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2016-02-10-profiling-top-kagglers-kazanova-new-1-in-the-world/3.png?raw=true">
  <figcaption>THE FINAL PRIVATE LEADERBOARD FOR THE VALUED SHOPPER'S CHALLENGE</figcaption>
</figure>

## What was your least favourite Kaggle competition experience?

[DecMeg](https://www.kaggle.com/c/decoding-the-human-brain), [BCI](https://www.kaggle.com/c/inria-bci-challenge) and such channel-wave type of competitions. They have big data and are very domain specific.

I found it hard to even make my CV working properly, plus I did quite bad. Hopefully I will improve.

## What field in machine learning are you most excited about?

I like recommender systems if it can be considered a separate field.

There is a broad spectrum of techniques you can use (which are field specific) and to be able to understand what the customer likes is very challenging and rewarding.

## Which machine learning researchers do you study?

I study: [Steffen Rendle](http://www.kaggle.com/users/25112/steffen-rendle), [Leo Breiman](https://www.stat.berkeley.edu/~breiman/), [Alexander Karatzoglou](http://www.ci.tuwien.ac.at/~alexis/About.html), [Michael Jahrer](https://www.kaggle.com/users/1455/michael-jahrer) & [Andreas Töscher](http://www.researchgate.net/profile/Andreas_Toescher), the [Machine Learning and Data Mining Group](http://www.csie.ntu.edu.tw/~cjlin/mlgroup/) at National Taiwan University, and [Jun Wang](http://web4.cs.ucl.ac.uk/staff/jun.wang/blog/about/) & [Philip Treleaven](http://www0.cs.ucl.ac.uk/staff/p.treleaven/).

## Can you tell us something about the last algorithm you hand-coded?

It was [LibFM](http://www.libfm.org/) for [Avazu](https://www.kaggle.com/c/avazu-ctr-prediction) competition as I believed it could work well in that particular problem. I could not make it work as well as [LibFFM](http://www.csie.ntu.edu.tw/~cjlin/libffm/) apparently.

## How important is domain expertise for you when solving data science problems?

For some competitions it is really important.

The fact that I am employed in the recommendation science field and the kind of work that we do within my team, has helped me win the Acquire valued Shoppers challenge.

However I think you can go a long way by following standard approaches even if you don't know the field well, which is also the beauty of machine learning and the fact that some algorithms do a significant job for you.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2016-02-10-profiling-top-kagglers-kazanova-new-1-in-the-world/4.png?raw=true">
</figure>

## What do you consider your most creative trick/find/approach?

I do multiple ensemble meta-stacking if I can use the term.

During the course of my univariate model tuning I save all the models' outputs. Then I make meta-models with the univariate models selections and most of the times I end up with different ensembles of Meta models.

Sometimes I go to third Meta model with Meta models as inputs (Meta-Meta model).

## How are you currently using data science at work and does competing on Kaggle help with this?

**Classified!**

Kaggle does help in optimizing my methods, learning new skills, meet nice people with same passion, be up to date with new tools and generally stay in touch with what's going on in the field.

## What is your opinion on the trade-off between high model complexity and training/test runtime?

That is a big discussion in principle.

I guess there is a trade-off, but there needs to be an understanding that better models are not necessarily the most interpretable ones and that a more complex model (that is likely to score better) is not necessarily less stable/more dangerous.

I guess the optimum solution should be somewhere in the middle (e.g. not an ensemble of 100 models nor Naive Bayes)

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2016-02-10-profiling-top-kagglers-kazanova-new-1-in-the-world/5.png?raw=true">
  <figcaption>THE BEST 8 FINISHES FOR KAZANOVA.</figcaption>
</figure>


## How did you get better at Kaggle competitions?

Did I ?! 😀

I guess what has helped a lot is:

1. Seeing previous solutions and end-of-competition threads
2. Participate in Kaggle forums
3. Learn the tools
4. Read papers, websites, machine learning tutorials
5. Optimize processes (use sparse matrices, cut unnecessary steps, write more efficient code)
6. Save everything I've done and reuse (and improve). E.g. I keep a separate folder for each competition I've completed.
7. Dedicate time (had to reduce video games)
8. Collaborate with others

I have found the following resources useful:

1. This [benchmark](http://www.kaggle.com/c/amazon-employee-access-challenge/forums/t/4797/starter-code-in-python-with-scikit-learn-auc-885) by [Paul Duan](https://www.kaggle.com/users/44623/paul-duan) in the [Amazon competition](https://www.kaggle.com/c/amazon-employee-access-challenge) (my first ever attempt with Python) for a general modelling framework.
2. From the same competition : [Python code to achieve 0.90 AUC with logistic regression](http://www.kaggle.com/c/amazon-employee-access-challenge/forums/t/4838/python-code-to-achieve-0-90-auc-with-logistic-regression) from [Miroslaw Horbal](https://www.kaggle.com/users/66023/miroslaw-horbal) to create pairwise interactions with cross-validation.
3. For text analysis, this benchmark from [Abhishek](https://www.kaggle.com/users/5309/abhishek): [Beating the benchmark](http://www.kaggle.com/c/stumbleupon/forums/t/5680/beating-the-benchmark-leaderboard-auc-0-878) in [StumbleUpon Evergreen Challenge](https://www.kaggle.com/c/stumbleupon)
4. [XGBoost benchmark](http://www.kaggle.com/c/higgs-boson/forums/t/8184/public-starting-guide-to-get-above-3-60-ams-score) in [Higgs Boson competition](https://www.kaggle.com/c/higgs-boson) by [Bing Xu](https://www.kaggle.com/users/43581/bing-xu)
5. [Tinrtgu](https://www.kaggle.com/users/185835/tinrtgu)'s [FTRL](http://jmlr.org/proceedings/papers/v15/mcmahan11b/mcmahan11b.pdf) Logistic model in Avazu: [Beat the benchmark with less than 1MB of memory](http://www.kaggle.com/c/avazu-ctr-prediction/forums/t/10927/beat-the-benchmark-with-less-than-1mb-of-memory)
6. [Data science Bowl](https://www.kaggle.com/c/datasciencebowl) tutorial for image classification: [IPython Notebook Tutorial](http://nbviewer.ipython.org/github/udibr/datasciencebowl/blob/master/141215-tutorial.ipynb).
7. [H2O](http://0xdata.com/) (R) [deep learning benchmark](https://www.kaggle.com/c/afsis-soil-properties/forums/t/10568/ensemble-deep-learning-from-r-with-h2o-starter-kit) from [Arno Candel](https://www.kaggle.com/users/234686/arno-candel) in [Africa Soil competition](https://www.kaggle.com/c/afsis-soil-properties)
8. [Lasagne and nolearn tutorial](http://nbviewer.ipython.org/github/ottogroup/kaggle/blob/master/Otto_Group_Competition.ipynb) for [Otto competition](https://www.kaggle.com/c/otto-group-product-classification-challenge) (by the admin) :
9. Andrew Ng's [Coursera course in Machine learning](https://www.coursera.org/course/ml)
10. University of Utah [Machine learning slides](http://www.cs.utah.edu/~piyush/teaching/cs5350.html).
11. Wikipedia and Google

## Are partnerships important in achieving good results?

Very.

Sometimes you cannot measure the impact from one competition only as what you learn from the others may be applicable in the future too. I've been very lucky to have made good and fun collaborations so far and I have learnt from all, especially:

1. From [Gert](https://www.kaggle.com/users/9974/gert) I've learnt model ensembling, feature engineering and Fourier transforms.
2. [Triskelion](https://www.kaggle.com/users/114978/triskelion) and [Phil Culliton](https://www.kaggle.com/users/115173/phil-culliton): [Vowpal Wabbit](http://hunch.net/~vw/)
3. [TVS](https://www.kaggle.com/users/111641/tvs) to avoid over-fitting
4. [Bluefool](https://www.kaggle.com/users/2242/bluefool) (or Domcastro) 1st derivatives and [BART](http://www.stat.rice.edu/~jrojo/4th-Lehmann/slides/mcculloch.pdf)
5. [Mike](https://www.kaggle.com/users/38878/mike), Python!
6. [Giulio](https://www.kaggle.com/users/111776/giulio), competition management and [Lasagne](https://github.com/Lasagne/Lasagne).

I am SO PROUD that I had the honour/chance/opportunity to play, learn and exchange bits and bytes with Kagglers, like:

[Gert](https://www.kaggle.com/gertjac), [Triskelion](https://www.kaggle.com/triskelion/), [Yan Xu](https://www.kaggle.com/yansoftware), [SRK](https://www.kaggle.com/sudalairajkumar), [Rafael](https://www.kaggle.com/potamitis), [Faron](https://www.kaggle.com/mmueller), [Clobber](https://www.kaggle.com/clobber), [Bluefool](https://www.kaggle.com/domcastro), [Mark Landry](https://www.kaggle.com/mlandry), [Giulio](https://www.kaggle.com/adjgiulio), and [Abhishek](https://www.kaggle.com/abhishek)

I would keep monitoring their progress 🙂 .

## Bio

[Marios Michailidis](https://www.linkedin.com/pub/marios-michailidis/21/665/326/) is Manager of Data science in dunnhumby and part-time PhD in machine learning at University College London (UCL) with a focus on improving recommender systems. He has worked in both marketing and credit sectors in the UK Market and has led many analytics projects with various themes including: Acquisition, Retention, Uplift, fraud detection, portfolio optimization and more. In his spare time he has created [KazAnova](http://www.kazanovaforanalytics.com/software.html), a GUI for credit scoring 100% made in Java.

Marios loves competing on Kaggle and learning new machine learning tricks. He told us he will create something good for the ML community soon...
