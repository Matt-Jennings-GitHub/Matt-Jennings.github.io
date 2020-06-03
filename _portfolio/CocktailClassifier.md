---
title: "Cocktail Classifier App"
date: 2020-06-02
tags: [physics, optics, numcerical modelling]
header:
  image: "/images/skyline.jpg"
  teaser: "/images/CocktailClassifier/CocktailClassifierTh.png"
excerpt: "Image Recognition, Neural Network"
mathjax: true
---

A fun app to predict the type of cocktail present in an image, using a convolution neural network trained on thousands of images web-scraped from Google Images!

## Demonstration

<img src="{{ site.url }}{{ site.baseurl }}/images/CocktailClassifier/Cocktails.png" alt="Cocktail Classifier App Demonstration">

Based on its training data, the app assigns a probability to each type of cocktail.

## How it works

We make use of a convolutional neural network: a deep learning model which can very effectivley capture patterns and shapes present in the image pixel data to make a prediction.

Transfer learning is used, with our feature selector as the VGG16 model pretrained on the ImageNet dataset. An additional dense layer with 256 neurons is added to the network and fed into our output layer with 13 neurons, each corresponding to a drink type we seek to classify.

```python
# Drink Types
classes = ['beer','bloody_mary','cosmopolitan','espresso_martini','gin_and_tonic','manhattan','margarita','martini','mojito','old_fashioned','rum_and_coke','pina_colada','screwdriver']
# Transfer Model
pretrained_network = vgg16.VGG16(weights='imagenet', include_top=False, input_shape=(target_size[0], target_size[1], 3))
# Extended Network
model = Sequential()
model.add(Flatten(input_shape=x_train_features.shape[1:], name='Flatten_Layer'))
model.add(Dense(256, activation='relu', name='Final_Hidden_Layer'))
model.add(Dropout(0.3))
model.add(Dense(len(classes), activation='softmax', name='Output_Layer'))
# Compile Network
model.compile(loss='categorical_crossentropy', optimizer='adam')
```
Here, we use the Keras wrapper for TensorFlow to impliment the sequential network.

The extended network was trained to recognise drinks by examining the 1000 images of each beverage, web scraped from Google Images. The training images were passed through a preprocessing script, which attempts to filter out image noise before compressing each picture into a 75x75 array, for consistent passes through the network layers. Below is a sample of training data for the Espresso Martini class:

<img src="{{ site.url }}{{ site.baseurl }}/images/CocktailClassifier/EspressoMartinis.PNG" alt="Sample Training Data">

Using the trained network, we can then predict what is present in the image, by assigning a probability to the follwing classes:
- Beer
- Bloody Mary
- Cosmopolitan
- Espresso Martini
- Gin and Tonic
- Manhattan
- Margarita
- Martini
- Mojito
- Old Fashioned
- Rum and Coke
- Pina Colada
- Screw Driver

## Limitations

Although web scraping the top 1000 pictures in each class from Google Images is a fast and effective way to obtain training data, the images are subject to a lot of variation, leading to potential loss in accuracy.

As an example, searching for a Martini will also yield many photos of an Espresso Martini, resulting in the miss-classification shown in the demonstration above.

<img src="{{ site.url }}{{ site.baseurl }}/images/CocktailClassifier/SearchResults.PNG" alt="Martini Google Search Results">

Note how many of the google results show espresso martinis instead! The full source code for the image preprocessor and CNN, along with further details, can be found on my [GitHub](https://github.com/Matt-Jennings-GitHub).
