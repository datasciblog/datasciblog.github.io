---
layout: single
title:  "The Simplest Way to Build an App with Your Deep Learning Model"
date:   2019-12-26
permalink: /2019/12/26/building-app/
excerpt: ""
categories: 
- Deep Learning
tags:
- deployment
- streamlit
- heroku
classes: wide
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

# Introduction

Training a deep learning model is cool, putting it into production is even cooler. 

As a student who had changed from a business background to data science, I always found it difficult to learn and do any IT stuff. That was the reason why during nearly two years of studying my master degree at Monash, I had been avoiding the question "What's next after training a machine learning model?". At that moment, I knew I should somehow make my model alive by taking further steps - putting it into a mobile or web application. But the idea of learning any web/app framework while there were a lot of assignments due just discouraged me. 

Fortunately, I had [Streamlit](https://streamlit.io/) and [Heroku](https://www.heroku.com/).  While, Streamlit is an app framework which enables you writing an app without leaving your Jupyter Notebook, Heroku's platform gives you the simplest path to deliver your apps quickly. 

# Building Application

## 1. Train a model and export it

For the purpose of introducing Streamlit and Heroku, I assume that you already have trained a model and exported it using **fastai** library.

Don't know how to do it? Check out these lessons:

- Fast.ai lesson 1: [How to train a pet classifier with resnet34 architecture](https://course.fast.ai/videos/?lesson=1)
- Fast.ai lesson 2: [How to create your own image dataset and build a classifier](https://course.fast.ai/videos/?lesson=2)

## 2. Build a Streamlit app and run it locally

### Install `streamlit` on your environment

```
$ pip install streamlit
```

### Create `app.py` file

- **Import all libraries we need**

```python
        from fastai.vision import open_image, load_learner, image, torch
        import streamlit as st
        import numpy as np
        import matplotlib.image as mpimg
        import os
        import time
        import PIL.Image
        import requests
        from io import BytesIO
```

- **Create the app title with `st.title`**

```python
        # App title
        st.title("Son Tung MTP vs G-Dragon")
```

- **Define the function that loads the model and make prediction**

    - `load_learner` : loads the trained model `export.pkl` inside the given folder
    - `st.image` : displays an image within the app
    - `st.spinner` : displays a message while executing
    - `st.success` : displays a success message

    ![https://raw.githubusercontent.com/trungha-ngx/MTP-vs-GD/master/gif/messages.gif](https://raw.githubusercontent.com/trungha-ngx/MTP-vs-GD/master/gif/messages.gif)

```python
        def predict(img, display_img):
        
            # Display the test image
            st.image(display_img, use_column_width=True)
        
            # Temporarily displays a message while executing 
            with st.spinner('Wait for it...'):
                time.sleep(3)
        
            # Load model and make prediction
            model = load_learner('model/data/train/')
            pred_class = model.predict(img)[0] # get the predicted class
            pred_prob = round(torch.max(model.predict(img)[2]).item()*100) # get the max probability
            
            # Display the prediction
            if str(pred_class) == 'mtp':
                st.success("This is Son Tung MTP with the probability of " + str(pred_prob) + '%.')
            else:
                st.success("This is G-Dragon with the probability of " + str(pred_prob) + '%.')
```

- **Let user choose the source of input images with `st.option`**

```python
        option = st.radio('', ['Choose a test image', 'Choose your own image'])
```

    - If they want to use a given test image, let them choose one from the list:

```python
        `st.selectbox` : displays a list of choice

            if option == 'Choose a test image':
            
                # Test image selection
                test_images = os.listdir('model/data/test/')
                test_image = st.selectbox(
                    'Please select a test image:', test_images)
            
                # Read the image
                file_path = 'model/data/test/' + test_image
                img = open_image(file_path)
            
                # Get the image to display
                display_img = mpimg.imread(file_path)
            
                # Predict and display the image
                predict(img, display_img)
```

        ![https://raw.githubusercontent.com/trungha-ngx/MTP-vs-GD/master/gif/choice_1.gif](https://raw.githubusercontent.com/trungha-ngx/MTP-vs-GD/master/gif/choice_1.gif)

    - Else, they want to use their own image, let them input the url:

```python
        `st.text_input` : displays a single-line text input widget

            else:
                url = st.text_input("Please input a url:")
            
                if url != "":
                    try:
                        # Read image from the url
                        response = requests.get(url)
                        pil_img = PIL.Image.open(BytesIO(response.content))
                        display_img = np.asarray(pil_img) # Image to display
            
                        # Transform the image to feed into the model
                        img = pil_img.convert('RGB')
                        img = image.pil2tensor(img, np.float32).div_(255)
                        img = image.Image(img)
            
                        # Predict and display the image
                        predict(img, display_img)
            
                    except:
                        st.text("Invalid url!")
```

        ![https://raw.githubusercontent.com/trungha-ngx/MTP-vs-GD/master/gif/choice_2.gif](https://raw.githubusercontent.com/trungha-ngx/MTP-vs-GD/master/gif/choice_2.gif)

- **Run the app locally**

```
        $ streamlit run app.py
```

    ![https://raw.githubusercontent.com/trungha-ngx/MTP-vs-GD/master/gif/run.gif](https://raw.githubusercontent.com/trungha-ngx/MTP-vs-GD/master/gif/run.gif)

## 3. Run your app publicly with Heroku

- **Create `Procfile` and `requirements.txt` files**
    - For `Procfile`, it requires only one line. Note that the file has no extention.

```
            web: streamlit run --server.enableCORS false --server.port $PORT app.py
```

    - For `requirements.txt`, put all libraries needed to run your app

```
            streamlit
            matplotlib
            numpy
            https://download.pytorch.org/whl/cpu/torch-1.1.0-cp36-cp36m-linux_x86_64.whl
            fastai
```

- **Upload all your files to [Github](https://github.com/trungha-ngx/MTP-vs-GD)**

    <figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-12-26-building-app/0.png?raw=true">
	<figcaption></figcaption>
    </figure>
    
- **Create a [Heroku account](https://signup.heroku.com/). It's free**
- **Go to [Heroku dashboard](https://dashboard.heroku.com/apps) and create a new app**

    <figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-12-26-building-app/1.png?raw=true">
	<figcaption></figcaption>
    </figure>

    Give it a name

    <figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-12-26-building-app/2.png?raw=true">
	<figcaption></figcaption>
    </figure>

    Connect the app to your GitHub repo

    <figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-12-26-building-app/3.png?raw=true">
	<figcaption></figcaption>
    </figure>

    Deploy it and wait a minute

    <figure>
	<img src="https://github.com/datasciblog/datasciblog.github.io/blob/master/_posts/images/2019-12-26-building-app/4.png?raw=true">
	<figcaption></figcaption>
    </figure>

- **Boom! Your app is ready for public use.**

    [Streamlit](https://mtp-vs-gd.herokuapp.com/)