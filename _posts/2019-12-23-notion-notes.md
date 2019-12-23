---
layout: single
title:  "Notion Notes"
date:   2019-12-23
permalink: /2019/12/23/notion-notes/
excerpt: ""
categories: 
- Deep Learning
tags:
- deep learning specialization
- coursera
classes: wide
#toc: true
#toc_label: "Table of Contents"
#toc_icon: "cog"
---

# Lesson 1

Class: Fast.ai
Created: Dec 23, 2019 12:13 PM
No: 2
Reviewed: No
Tags: CNN, ResNet
Type: Lecture, Tutorial

# Resources

- Lecture

[Fast AI Video Viewer](https://course.fast.ai/videos/?lesson=1)

- Notebook

[fastai/course-v3](https://github.com/fastai/course-v3/blob/master/nbs/dl1/lesson1-pets.ipynb)

- Summary

[hiromis/notes](https://github.com/hiromis/notes/blob/master/Lesson1.md)

- DAWNBench

[DAWNBench](https://dawn.cs.stanford.edu/benchmark/)

# Takeaways

- Pick one project, do it really well, make it fantastic
- Try to train models on your own data

# Key Concepts

- Transfer Learning:
    - Use weights from pre-trained models which have learnt something rather than train a new model from begining
- [ResNet](https://www.notion.so/trunghanguyen/Deep-Residual-Learning-for-Image-Recognition-2ebdfaddac0a4eca9383673120bdfb37): Residual Neural Networks
    - ResNet34
    - ResNet50: Best in [benchmark](https://dawn.cs.stanford.edu/benchmark/)
- Validation Set:
    - Compulsory when training models to avoid overfitting
- [One-Cycle Policy Fitting](https://www.notion.so/trunghanguyen/A-disciplined-approach-to-neural-network-hyper-parameters-Part-1-learning-rate-batch-size-mome-53c2eaf58cea4cd4aeadd80c81f2c4ed)

# Preparing Data

There are many ways to create data with ImageDataBunch. Try `doc(ImageDataBunch)`for more details.

## Codes

    bs = 64
    
    path = untar_data(URLs.PETS); path
    path.ls()
    
    path_anno = path/'annotations'
    path_img = path/'images'
    
    fnames = get_image_files(path_img)
    
    # Try other method to create ImageDataBunch objects
    np.random.seed(2)
    pat = r'/([^/]+)_\d+.jpg$'
    data = ImageDataBunch.from_name_re(path_img, fnames, pat, ds_tfms=get_transforms(), size=224, bs=bs)
    data = data.normalize(imagenet_stats)
    
    data.show_batch(rows=3, figsize=(7,6))
    
    print(data.classes)
    len(data.classes), data.c

# Training Models

## Codes

    learn = cnn_learner(data, models.resnet34, metrics=error_rate)
    learn.model # Summary of the model
    
    learn.fit_one_cycle(4)
    learn.save('stage-1')