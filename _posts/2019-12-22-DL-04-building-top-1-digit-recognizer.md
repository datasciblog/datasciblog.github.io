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