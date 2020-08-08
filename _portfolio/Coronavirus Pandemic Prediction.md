---
title: "Coronavirus Pandemic Prediction"
date: 2020-08-08
tags: [data science, machine learning, data visualization]
header:
  image: "/images/skyline.jpg"
  teaser: "/images/CoronavirusPrediction/CoronavirusPredictionTh.jpg"
excerpt: "Pandemic Prediction with Machine Learning"
mathjax: true
---

Predicting and understanding the spread of the COVID-19 Pandemic in the USA can help forcast supply chains and save jobs and lives. The reproduction number is first predicted using estimates based on the SIRf pandemic model. Geographic, Socioeconomic and Health factors from individual counties are sourced and analysed from USA government datasets. These factors are used in machine learning models to predict the spread of the virus. Finally, the results are visualised geographically. 

## Predictions made

<img src="{{ site.url }}{{ site.baseurl }}/images/CoronavirusPrediction/PredictionsComparison.gif" alt="Model Predictions">

## Calculaing the reproduction number (*R*)

<img src="{{ site.url }}{{ site.baseurl }}/images/SIRf-Model/SIRf-Model.png" alt="ExampleSIRf Model Predictions">

Predictions are made with the following set of coupled ODEs,

$$\frac{dy}{dz} = by(1-z) - \frac{y}{T}$$

$$\frac{dz}{dt} = by(1-z)$$

$$D = NPaz(t-1)$$

where $$b = \frac{R}{T}$$ .

See my post on [SIRf Modelling](http://mattjennings.ddns.net/portfolio/COVID-19%20SIR-Modelling/) for more details on this model. Other trialled estimates of R included taking ratios of daily case data.

## Data Sources
