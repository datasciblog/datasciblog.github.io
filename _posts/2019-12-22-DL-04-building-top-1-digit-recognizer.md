---
layout: single
title:  "Building Top 1% Digit Recognizer"
date:   2019-12-22
permalink: /2019/12/22/building-top-1-digit-recognizer/
excerpt: ""
categories: 
- Deep Learning
tags:
- deep learning
- kaggle
- image classification
classes: wide
#toc: true
#toc_label: "Table of Contents"
#toc_icon: "cog"
---

# Import Library

```python
	# Import libraries
	%matplotlib inline

	import numpy as np
	import pandas as pd
	import matplotlib.pyplot as plt
	from sklearn.model_selection import train_test_split
	import time

	import torch
	import torch.nn as nn
	import torch.nn.functional as F
	from torch.utils.data import DataLoader, Dataset, ConcatDataset
	from torchvision import transforms
	import torch.optim as optim
```

# Import Data

```python
	# Read csv files
	train_df = pd.read_csv('/kaggle/input/digit-recognizer/train.csv')
	test_df = pd.read_csv('/kaggle/input/digit-recognizer/test.csv')
	submit_df = pd.read_csv('/kaggle/input/digit-recognizer/sample_submission.csv')
```

```python
	# Number of pixels
	num_pixel = len(train_df.columns) - 1
	num_pixel
```

# Argumentation, Datasets and DataLoaders

```python
	# Transformers
	transform_0 = transforms.Compose([
		transforms.ToPILImage(),
		transforms.ToTensor(),
		transforms.Normalize([0.5], [0.5])
	])

	transform_1 = transforms.Compose([
		transforms.ToPILImage(),
		transforms.RandomRotation(30),
		transforms.ToTensor(),
		transforms.Normalize([0.5], [0.5])
	])

	transform_2 = transforms.Compose([
		transforms.ToPILImage(),
		transforms.RandomAffine(degrees=15, translate=(0.1,0.1), scale=(0.8,0.8)),
		transforms.ToTensor(),
		transforms.Normalize([0.5], [0.5])
	])

	transform_3 = transforms.Compose([
		transforms.ToPILImage(),
		transforms.RandomAffine(degrees=30, scale=(1.1,1.1)),
		transforms.ToTensor(),
		transforms.Normalize([0.5], [0.5])
	])

	transform_4 = transforms.Compose([
		transforms.ToPILImage(),
		transforms.RandomAffine(degrees=30, translate=(0.1,0.1)),
		transforms.ToTensor(),
		transforms.Normalize([0.5], [0.5])
	])

	transform_5 = transforms.Compose([
		transforms.ToPILImage(),
		transforms.RandomAffine(degrees=10, shear=45),
		transforms.ToTensor(),
		transforms.Normalize([0.5], [0.5])
	])
```


```python

```

```python

```

```python

```

```python

```