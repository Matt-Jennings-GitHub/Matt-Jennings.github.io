---
title: "Diffraction Modelling"
date: 2020-06-02
tags: [physics, optics, numcerical modelling]
header:
  image: "/images/skyline.jpg"
  teaser: "/images/DiffractionModelling/DiffractionModellingTh.jpg"
excerpt: "Optical Phyics, Numerical Modelling"
mathjax: true
---

Using a numerical approximation of the Fourier Transform, we predict the resulting diffraction patterns produced from optical diffraction experiements with various shaped 2D sources in matrix representation.

##Background

Optical signals are rarely monochromatic but rather a superposition of characteristic frequencies. These can be expressed as a Fourier Series of sine and cosine functions through the Fourier Series:

$$F\left(u,v\right)=\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}{f\left(x,y\right)e^{-2\pi i(xu+yv)}}dxdy$$

In 2 dimensions and used to demonstrate the diffraction patterns of a cross-shaped aperture and double slit source.


## Sample Output

<img src="{{ site.url }}{{ site.baseurl }}/images/SIRf-Model/SIRf-Model.png" alt="SIRf Model Predictions">

Predictions are made with the following set of coupled ODEs,

$$\frac{dy}{dz} = by(1-z) - \frac{y}{T}$$

$$\frac{dz}{dt} = by(1-z)$$

$$D = NPaz(t-1)$$

where $$b = \frac{R}{T}$$ .

These are integrated with the SciPi ODE Integrator:

```python
# Integrate the model with SciPi ODE Integrator
xt = odeint(SIRf, x0, t, args=(b, T))
```

## SIR Model

Parameters:
- *y(t)*  Proportion of population who are infectious
- *z(t)* Proportion of initial population no longer susceptible to infection (dead, infected or recovered)
- *D(t)*  Total deaths
- *t*  Time since outbreak began
- **R**  Basic reproduction number 
- *T*  Average infectious period 
- *b*  Average number of people infected by an infectious individual per day (R/T)
- *l*  Average time between infection and death 
- *a*  Probability of dying with severe disease 
- *p*  Proportion of population at risk of severe disease 
- *N*  Size of population

See source code on my [GitHub](https://github.com/Matt-Jennings-GitHub) for parameter values used.