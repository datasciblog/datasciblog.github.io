---
layout: single
title:  "Stacking Made Easy: An Introduction to StackNet by Competitions Grandmaster Marios Michailidis (KazAnova)"
date:   2017-06-15
permalink: /2017/06/15/stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/
excerpt: ""
categories: 
- Stacking
tags:
- kaggle
- ensemble
classes: wide
# toc: true
# toc_label: "Table of Contents"
# toc_icon: "cog"
---

[Original Post](http://blog.kaggle.com/2017/06/15/stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/)

---

You’ve probably heard the adage “two heads are better than one.” Well, it applies just as well to machine learning where the combination of diverse approaches leads to better results. And if you’ve followed Kaggle competitions, you probably also know that this approach, called stacking, has become a staple technique among top Kagglers.

In this interview, [Marios Michailidis](https://www.kaggle.com/kazanova) (AKA Competitions Grandmaster KazAnova on Kaggle) gives an intuitive overview of stacking, including its rise in use on Kaggle, and how the resurgence of neural networks led to the genesis of his stacking library introduced here, StackNet. He shares how to make StackNet–a computational, scalable and analytical, meta-modeling framework–part of your toolkit and explains why machine learning practitioners shouldn’t always shy away from complex solutions in their work.

Have questions about stacking, StackNet, or Marios' illustrious career on and off Kaggle? *[He's holding an AMA (Ask Me Anything) on the Kaggle Forums](https://www.kaggle.com/general/34802)*.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2017-06-15-stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/1.png?raw=true">
  <figcaption>MARIOS (AKA KAZANOVA) ON KAGGLE.</figcaption>
</figure>

# Overview of Stacking and StackNet

## Can you give a brief introduction to stacking and why it’s important?

Stacking or Stacked Generalization is the process of combining various machine learning algorithms using holdout data. It is attributed to [Wolpert 1992](http://www.machine-learning.martinsewell.com/ensembles/stacking/Wolpert1992.pdf). It normally involves a four-stage process. Consider 3 datasets A, B, C. For A and B we know the ground truth (or in other words the target variable y). We can use stacking as follows:

1. We train various machine learning algorithms (regressors or classifiers) in dataset A
2. We make predictions for each one of the algorithms for datasets B and C and we create new datasets B1 and C1 that contain only these predictions. So if we ran 10 models then B1 and C1 have 10 columns each.
3. We train a new machine learning algorithm (often referred to as Meta learner or Super learner) using B1
4. We make predictions using the Meta learner on C1

Still confusing? Consider this animation:

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2017-06-15-stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/2.gif?raw=true">
</figure>

For a large scale implementation of stacking, one may further read or use [stacked ensembles](https://h2o-release.s3.amazonaws.com/h2o/rel-ueno/2/docs-website/h2o-docs/data-science/stacked-ensembles.html).

Stacking is important because (experimentally) it has been found to **improve performance** in various machine learning problems. I believe most winning solutions on Kaggle the past 4 years included some form of stacking.

Additionally, the advent of **increased computing power** and parallelism has made it possible to run many algorithms together. Most algorithms rely on certain parameters or assumptions to perform best, hence each one has advantages and disadvantages. Stacking is a mechanism that tries to leverage the benefits of each algorithm while disregarding (to some extent) or correcting for their disadvantages. In its most abstract form, stacking can be seen as a mechanism that corrects the errors of your algorithms.

## Great, so what is StackNet?

**StackNet** is a computational, scalable and analytical, meta-modeling framework implemented in Java that resembles a feedforward neural network and uses Wolpert’s stacked generalization on multiple levels to improve accuracy in machine learning predictive problems.

StackNet was created as part of my PhD at UCL which was sponsored by dunnhumby. It can be downloaded from the [GitHub repo](https://github.com/kaz-Anova/StackNet):

The supervisors are:
- Giles Pavey
- Prof. Philip Treleaven

Breaking down the definition of StackNet to its basic rudiments we have:

1. **Computational**: Because it involves heavy computing.
2. **Scalable**: Because many models can be run in parallel. More threads lead to faster results.
3. **Analytical**: Because it is heavily based on the principles of data analysis (or data science), especially when it comes to data preprocessing, cross validating, measuring performance through various metrics.
4. **Meta-modelling**: Because it uses the notion of meta learners. In other words, it uses predictions of some algorithms as features to other algorithms.
5. **Wolpert’s stacked generalization**: Because the meta-learners are created using this technique of combining predictions in hold-out datasets.
6. **Feedforward neural network and multiple levels**: Because stacking is not limited to just the 4 stages mentioned in the stacking section, but have the ability to be repeated multiple times creating more datasets from predictions (like B2,C2…until Bn,Cn).
7. **Java**: Because the first implementation of StackNet is in the Java programming language.

StackNet has (already) been used to win machine learning challenges. A typical implementation may be viewed in [the winning solution of the Truly Native Kaggle challenge](http://blog.kaggle.com/2015/12/03/dato-winners-interview-1st-place-mad-professors/). In that challenge, the winning StackNet had 4 layers of meta (neuron) models to achieve the best score. The final architecture is illustrated below:

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2017-06-15-stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/3.jpg?raw=true">
</figure>

A typical neural network is commonly trained with a form of **back propagation**; however, stacked generalization–as stated before–requires a forward training methodology that splits the data **into 2 parts** (A and B)–one of which is used for training (A) and the other for predictions (B).

The reason this split is necessary is to **avoid over-fitting**. However, splitting the data in just 2 parts would mean that in each new layer in the second part needs to be further dichotomized or in general more datasets would be required (D,F…Z). This has the effect of increasing the bias of overfitting even more as each algorithm will have to be trained and validated on increasingly **less data**.

To overcome this drawback, the algorithm utilizes **a K-fold cross validation** (where K is a hyperparameter). This process implies that we split the data K times and run models to output predictions for each K part and then bring the K parts back together to the original order so that the output predictions can be used in later stages of the model. This process is illustrated below in figure

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2017-06-15-stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/4.jpg?raw=true">
</figure>

Optionally instead of predicting the test data at the same time for each K model, we may choose to train another algorithm on the whole training data (after K-fold is done). There is no reason to limit the ability of the model to learn using less than 100% of the training data since the output scoring is already unbiased.

***“I still don’t get it–why does building so many models on different levels help? Besides they look ‘ugly’. I prefer the era when building one good model was enough.”***

It is based on the principle that no model is perfect. Almost every time the models make mistakes. Plus, each model has different advantages and disadvantages and they tend to seize the data from different angles. Leveraging the uniqueness of each model is of the essence for building very predictive models.

I often like to explain stacking on multiple levels with the following (albeit simplistic) example:

Let’s assume there are three students named **LR**, **SVM**, **KNN** and they argue about a physics question where they have different opinions of what the right answer might be:

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2017-06-15-stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/5.png?raw=true">
</figure>

They decide there is no way to convince one another about their case and they do the democratic thing via taking an **average** of their estimates which is this case is **14**. They used one of the simplest form of ensembling – AKA **model averaging**.

Their teacher, Miss DL–a maths teacher–bears witness to the argument the students are having and decides to help. She asks “what was the question?”, but the students refuse to tell her (because they know it is not in their benefit to give all the information, besides they think she might find silly they are arguing for such a trivial matter). However they do tell her that it is a physics related argument.

In this scenario, the teacher does not have access to the initial data as she does not know what the question was. However she does know the students very well–their **strengths** and **weakness** and she decides she can still help in solving this matter. Using historical information of how well the students have done in the past, plus the fact that she knows SVM loves physics and always does well in this subject (plus her father worked in a physics institute of excellence for young scientists), she thinks the most appropriate answer would be more like **17**.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2017-06-15-stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/6.png?raw=true">
</figure>

In this instance the teacher (DL) is a **meta learner**. She uses as input data the results of what other models (the students) are outputting. Then she combines it with historical information of how well the students have done in the past to get a better estimate (and help resolve the conflict).

However... **Mr RF**, a physics teacher has a slightly different opinion. He was there the whole time, but he waited until this moment to make his move! Mr RF has been teaching LR private lessons in physics lately to boost his grades (something that miss DL did not know) and he thinks LR’s contribution to the final estimate should be bigger. Therefore he claims the right answer to be more like **16**!

In this case Mr RF is **also a Meta learner** and he processes the historical data with different logic–plus he has access to additional sources (or different historical information) than Miss DL.

This dispute can only be resolved if **Headmaster GBM** makes a decision! GBM does not know what the children have said, but knows his teachers quite well and he is more keen to trust his physics teacher (RF). He concludes the answer to be more like **16.2**.

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2017-06-15-stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/7.png?raw=true">
</figure>

In this scenario the headmaster is **a level 2 meta learner** or a meta learner of meta learners and via processing historical information of his teachers he may still be able to provide a better estimate than a simple average of their results.

# The history of stacking and StackNet on Kaggle

## What’s the inspiration behind StackNet?

There were 4 main drives behind the idea of StackNet:

1. **To win**. When I first started competing on Kaggle, I was trying to come up with ideas to improve. I first tried something like stacked generalization in a bird classification challenge in 2013. This was my first top 10 result and I briefly explained my approach there, without really knowing that what I did was stacked-generalization–I just tried it out of intuition to get my best score. After this I learnt more about it and I tried to build a strategy to make the best of it–hence coming up with StackNet.

2. **To leverage my experience** in some areas. Before I started competing on kaggle, my hobby was to do predictive modelling in the credit sector. I had built a tool that helps to build credit scorecards–using various machine learning algorithms but with a focus on logistic regression and linear models. When I first joined kaggle, everything was about Random Forests and Gradient Boosting Machines and I quickly realised that my expertise was not enough to perform competitively in this environment. However I had spent quite a lot of time time developing methodologies and processes that could make these models work well and I was constantly trying to find ways to include them into my pipeline. StackNet was the process that allowed me to find use for these weaker models as they still add information in this multi-modeling context.

3. The return of neural networks – AKA **deep learning**. The architecture of deep learning and the notion of being able to build deep models scalably, boosted the idea of using it in tandem with stacked generalization.

4. **To build something novel and give back to the community**. I have learnt a lot from open source material, from people sharing tips, tricks, codes, methodologies. I have learnt a lot from Kaggle. I have seen it many times, people building tools and sharing it back to the community making everyone better and I wanted to do a small part towards that direction. In a way, it is like paying my debt to my (anonymous) mentors–to your everyday, friendly neighborhood data scientists/coders/programmers that via sharing have made this world a better place.

## How did your experiences competing on Kaggle shape the development of StackNet?

As I have already mentioned above, Kaggle was integral to developing StackNet as it was the product of trying to beat the state-of-the-art methodologies that are often applied on Kaggle among thousands of participants in order to win data science challenges. Apart from that I have learnt a lot from the participants (Kagglers) either from them posting in forums or kernels or via direct collaborations.

Also competing in 100+ diverse challenges in areas such as image classification, sound classification, retention, recommendations, credit, marketing, text, etc. meant building and experimenting with more than 100K machine learning models–Kaggle has provided a great data science playground to invent or improve techniques such as this. It won’t be extreme to say that StackNet is in a way a *Kaggle’s baby*!

Some people would claim that building so many or complex machine learning models is “a waste of resources” given that the chance of winning is low. I think they probably ignore the potential contribution to science and the personal development you experience as a data scientist via participating. Also what may seem complex today, may not be that complex tomorrow if there is a demand for it–see deep learning! Not to mention the apparent boost in connectivity with the professional market plus all the fun that comes out via competing. Even my current role at H2O was a product of developing StackNet and trying it on Kaggle, since the company already builds very innovative software (like [H2O-3](https://github.com/h2oai/h2o-3)) in the data science space and we got the chance to meet each other through this platform.

# Let's get technical: Using StackNet

## How to use StackNet

All the information required to run StackNet can be found in its [main GitHub repository](https://github.com/kaz-Anova/StackNet) along with [examples from Kaggle competitions](https://github.com/kaz-Anova/StackNet/tree/master/example) on how to get competitive scores.

In a few simple steps, what you need to do to run StackNet is:

1. Clone the repository with git clone https://github.com/kaz-Anova/StackNet.git or just download the StackNet.jar from the repo which is already compiled.

    - Optionally if you want XGBoost or other external tools apart from the .jar you also need the lib.zip file and unzip it in the same directory where the .jar is.

2. Make sure you have java 1.6 installed or higher.

3. Get a dataset and convert it to .libsvm format. You can see some examples of such format here, but in general it is [target_variable col0:value0 col1:value1 …. coln:valuen]

4. Consider the following command (in cmd) for training a regression problem. For simplicity all parameters have a new entry in the following list, but in reality they need to be space delimited as one long sequence:

    - `Java –jar stacknet.jar train` : tells to execute the .jar file and train a model
    - `task=regression` : we specify if we want regression or classification
    - `sparse=true` : means our data is in sparse (libsvm) format
    - `train_file=x.csv` : the name of the training file
    - `test_file=X_test.csv` : the name of the test file to make predictions for
    - `pred_file=pred.csv` : the name of the file containing the predictions for the test_file
    - `params=params.txt` : A file containing the structure of the StackNet, which and how many algorithms to use
    - `metric=rmse` : the metric to validate performance of algorithms per fold
    - `folds=5` : Number of K-folds
    - `seed=1` : random seed to replicate results
    - `threads=3` : number of models to run in parallel . Ideally should not exceed cores for best performance.
    - `model=model.mod` :name of the model file. If we want to use it later on for other predictions, we could dump it.

The params file has the following structure. Each line is a model. When there is an empty line then any new algorithm is used in the next level:

```
    LogisticRegression C:1 Type:Liblinear maxim_Iteration:100 scale:true verbose:false
    RandomForestClassifier bootstrap:false estimators:100 threads:5
    GradientBoostingForestClassifier estimators:100 shrinkage:0.05
    LSVC Type:Liblinear threads:1 C:1.0 maxim_Iteration:100 seed:1
    LibFmClassifier lfeatures:3 init_values:0.035 smooth:0.05 learn_rate:0.1
    NaiveBayesClassifier usescale:true threads:1 Shrinkage:0.1 seed:1 verbose:false
    XgboostRegressor booster:gbtree objective:reg:linear num_round:100 eta:0.015
    RandomForestClassifier estimators=1000 rounding:3 threads:4 max_depth:6
```

**Tip**: To tune a single model, one may choose an algorithm for the first layer and a dummy one for the second layer. StackNet expects at least two algorithms, so with this format the user can visualize the performance of single algorithm inside the K-fold. For example, if I wanted to tune a Random Forest Classifier, I would put it in the first line (layer) and also put any model (let’s say Logistic Regression) in the second layer and could break the process immediately after the first layer kfold is done:

```
    RandomForestClassifier bootstrap:false estimators:100 threads:5
    LogisticRegression verbose:false
```

All the [available algorithms and their advised tunable parameters](https://github.com/kaz-Anova/StackNet/blob/master/parameters/PARAMETERS.MD) are in the repo.

As a quick note, one should try a few diverse models. To my experience, a good stacking solution is often composed of at least:

- 2 or 3 GBMs (one with low depth, one with medium and one with high)
- 1 or 2 Random Forests (again as diverse as possible–one low depth, one high)
- 1 or 2 NNs (one deeper, one smaller)
- 1 linear model

There is a video presenting StackNet in [the data science festival in London 2017](https://www.youtube.com/watch?v=9Vk1rXLhG48) which features a top 10 submission using it in the [Amazon employee classification challenge](https://www.kaggle.com/c/amazon-employee-access-challenge). The [example details are here](https://github.com/kaz-Anova/StackNet/blob/master/example/example_amazon/EXAMPLE.MD). One may look after [minute 14 where StackNet is presented](https://youtu.be/9Vk1rXLhG48?t=963).


## Why Java ?

- Java is less verbose than C to write and therefore more suited for data scientists to use.
- It is very popular (as it is included in 3 billion devices).
- Can be used in any operating system without serious modifications or compilers.
- Statically typed and better defined than other languages, hence is more suited for development (in comparison to Python for instance).
- Also Java does not have tools with an easy python API like sklearn does. StackNet contains its own algorithms (as well as other implementations) and can be further used in development too. These algorithms included in StackNet have [sklearn-like APIs](http://scikit-learn.org/stable/modules/classes.html), (however most of them are NOT the same algorithms). In other words, using Java for this means people who use Java for their data analysis could benefit from such an API, therefore it potentially extends the reach of data science to more people.

## What’s next for StackNet? What algorithms and features can we look forward to?

The most immediate improvements will refer to extending its coverage with world-class machine learning tools (like the XGBoost that got recently added). StackNet will (almost) always give you a bit better than your best single model, so it is vital to include the best tools so that the strongest ensembles can be constructed.

Tools expected to be added soon are:

- [H2O algorithms](https://h2o-release.s3.amazonaws.com/h2o/rel-turan/4/docs-website/h2o-py/docs/modeling.html)
- [LightGBM](https://github.com/Microsoft/LightGBM)
- [LIBFFM](https://www.csie.ntu.edu.tw/~cjlin/libffm/)
- [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit/wiki)
- [Weka Algorithms](http://www.cs.waikato.ac.nz/ml/weka/)

If I could add other tools like the sklearn library that would have been great, but I am not sure how feasible is to be done efficiently from Java.

Other elements that are expected be added come from the following areas:

- Wrappers for other programming languages
- Data pre-processing
- Feature Selection
- Hyper parameter optimization and grid search
- Possibly model decompression (from ensemble back to simple model) - ensemble pruning
- Possibly GUI for easier usage

Additionally StackNet model will be presented at [infiniteconf 2017](https://skillsmatter.com/conferences/7983-infiniteconf-2017-the-conference-on-big-data-data-science-and-engineering#program) [6th-7th July]

## When may StackNet not work well?

StackNet can overfit when there are **strong temporal elements** in the data–in situations like predicting the stock market or when the test data seem like they have been drawn from a **different or altered distribution** in comparison to the train data. StackNet’s ability to exhaust information within the training data (through multiple algorithms) means may not do very well when the future is significantly different from the past.

## Do you have any advice on using StackNet outside of competitions?

The first thing to mention here is that organizations should not be afraid to use blackbox solutions. It is true that a StackNet model may be very complex and tough to understand, but this should not intimidate people. One should focus on its performance via setting up a **reliable testing framework**.

Obviously it takes some time to get used to the tool and learn most of the algorithms and their parameters but it is worth the investment if maximum prediction performance is sought. Since StackNet’s predict and train tasks are scalable, time could be reduced significantly.

Also by having the ability to control the size of the ensemble, an organization may find it easy to specify the right threshold of model complexity, performance and cost.

## How can readers contribute to the project? What kinds of contributions are you looking for?

Apart from reporting bugs, a great help would be for people to assist with making wrappers for other tools or programming languages. It would be great if they could use the implemented API for [estimators](https://github.com/kaz-Anova/StackNet/blob/master/src/ml/estimator.java), [classifiers](https://github.com/kaz-Anova/StackNet/blob/master/src/ml/classifier.java), and [regressors](https://github.com/kaz-Anova/StackNet/blob/master/src/ml/regressor.java) to add to this project.

General performance optimization advice is very welcome, too.

# Acknowledgments

## References to other similar work, projects, or blogs

- [Wolpert 1992](http://www.machine-learning.martinsewell.com/ensembles/stacking/Wolpert1992.pdf) Stacked generalization
- [xcessiv](https://github.com/reiinakano/xcessiv)
- [Deepwater-stacked ensembles](https://www.youtube.com/watch?v=vFzdVIzwJwY&t=4667s) video
- [Kaggle ensemble guide](https://mlwave.com/kaggle-ensembling-guide/)
- [Kaggler’s practical ensemble guide](http://blog.kaggle.com/2016/12/27/a-kagglers-guide-to-model-stacking-in-practice/)

## Special thanks to

Apart from my supervisors, I would like to thank:

- Obviously [dunnhumby](https://www.dunnhumby.com/) for supporting the project
- [UCL](https://www.ucl.ac.uk/) for the same reason
- My Kaggle buddies [Triskelion](https://www.kaggle.com/triskelion) and [Faron](https://www.kaggle.com/mmueller) for building thousands of stacked models together!
- My sister [Afroditi Michaildi](https://www.linkedin.com/in/afroditi-michailidi-445561a6/) for designing the logo

<figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2017-06-15-stacking-made-easy-an-introduction-to-stacknet-by-competitions-grandmaster-marios-michailidis-kazanova/8.png?raw=true">
  <figcaption></figcaption>
</figure>

# About the author

Marios Michailidis (KazAnova) is Research Data Scientist at H2O and part-time PhD student in machine learning at University College London (UCL) with a focus on ensemble modelling. He is the creator of StackNet and other freeware machine learning tools like KazAnova GUI. Marios is former Kaggle #1, having competed in over 100 Kaggle competitions to challenge himself, learn from the best, and improve his research work.