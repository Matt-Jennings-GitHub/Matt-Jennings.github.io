---
title: "COVID-19 SIRf Modelling"
date: 2020-05-10
tags: [modelling, data science]
header:
  image: "/images/SIRf-Model/SIRf-Model.png"
  teaser: "/images/skyline.jpg"
excerpt: "Statistical Modelling"
mathjax: true
---

Implementation of Oxford's Susceptible-Infectious-Recovered framework (SIRf) Coronavirus (CV19) tracking model. Uses SciPy's ODE integrator to integrate a set of coupled linear first order ODEs with adjustable population parameters. Includes option to modify the effective reproductive number ('R') of the virus to see the effect of lock-down measures.


## H2 Sample Output

<img src="{{ site.url }}{{ site.baseurl }}/images/SIRf-Model/SIRf-Model.png" alt="SIRf Model Predictions">

Predictions are made with the following set of coupled ODEs:

$$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$

```python
# Integrate the model with SciPi ODE Integrator
xt = odeint(SIRf, x0, t, args=(b, T))
```