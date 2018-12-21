---
title: Estimating Parameters of Probabilistic Neuron Models
date: 2018-12-20 15:29:10
tags:
- neurons
- applied math
- GLIF 
- statistics
- data analysis

categories:
- neuronal dynamics
---

neural data analysis problems:
- encoding: predict the spike trains of a neuron or population of neurons given an input
- decoding: estimate the stimulus from the spikes 

difficulties:
- neural responses are stochastic
- possible stimuli are many

# 1. Parameter optimization

- desiderata for any neuron model:
  - flexible and powerful enough
  - tractable
  - respect known physiolgy

Question: how does a stimulus $I(t)$ encoded by the neuron?

## 1.1 Linear Models

