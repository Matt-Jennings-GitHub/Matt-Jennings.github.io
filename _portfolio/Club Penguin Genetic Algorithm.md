---
title: "Club Penguin Genetic Algorithm"
date: 2019-09-01
tags: [modelling, data science]
header:
  image: "/images/skyline.jpg"
  teaser: "/images/ClubPenguin/clubpenguin1.jpg"
excerpt: "Machine Learning, Genetic Algorithm"
mathjax: true
---

<iframe width="640" height="360" src="https://www.youtube-nocookie.com/embed/t1ViDz0MnJE?controls=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe>

## About
Here, we teach a neural network to learn to play that classic Ice Fishing game from Club Penguin! 

We first try using a fully-connected recurrent network with LSTM nodes, trained on human gameplay. We then use the NEAT genetic algorithm to evolve the neural connections from scratch and watch the A.I. learn the desired behaviour itself over many generations.

Neural Networks are an incredibly powerful machine-learning technique which can be used to model extremely complex patterns and behaviours; so why not apply them to everyone's favourite childhood game!

## Reinforcement Learning

The network was evolved over 3 hours of genetic evolution with reinforcement learning, placing the agent in a test environment implimented in PyGame.

<img src="{{ site.url }}{{ site.baseurl }}/images/ClubPenguin/clubpenguin2.jpg" alt="Genetic Evolution>

More details of the algorithm specifics can be found on my GitHub.