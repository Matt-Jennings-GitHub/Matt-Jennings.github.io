---
title: "COVID-19 SIRf Modelling"
date: 2020-05-10
tags: [modelling, data science]
header:
  image: "/images/SIRf-Model/SIRf-Model.png"
  teaser: "/images/SIRf-Model/SIRf-Model.png"
excerpt: "Statistical Modelling"
mathjax: true
---

Implementation of Oxford's Susceptible-Infectious-Recovered framework (SIRf) Coronavirus (CV19) tracking model. Uses SciPy's ODE integrator to integrate a set of coupled linear first order ODEs with adjustable population parameters. Includes option to modify the effective reproductive number ('R') of the virus to see the effect of lock-down measures.


## Sample Output

<img src="{{ site.url }}{{ site.baseurl }}/images/SIRf-Model/SIRf-Model.png" alt="SIRf Model Predictions">

Predictions are made with the following set of coupled ODEs:

$$\frac{dy}{dz} = by(1-z) - \frac{y}{T}$$

```python
# Integrate the model with SciPi ODE Integrator
xt = odeint(SIRf, x0, t, args=(b, T))
```

## SIR Model

Parameters:
-*y(t)*  Proportion of population who are infectious
-*z(t)* Proportion of initial population no longer susceptible to infection (dead, infected, recovered)
-*D(t)*  Total deaths
-*t*  Time since outbreak began
-**R**  Basic reproduction number (2.25 or 2.75 ± 0.025)
-*T*  Average infectious period (4.5 ± 1 days)
-*b*  Average number of people infected by an infectious individual per day (R/T)
-*l*  Average time between infection and death (17 ± 2 days)
-*a*  Probability of dying with severe disease (0.14 ± 0.007)
-*p*  Proportion of population at risk of severe disease (0.01 or 0.001 ± 50%)
-*N*  Size of population (67 million)
