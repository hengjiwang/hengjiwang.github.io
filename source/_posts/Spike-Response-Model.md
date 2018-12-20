---
title: Spike Response Model
date: 2018-12-19 23:26:53
tags:
- neurons
- dynamics
- GLIF
categories:
- neuronal dynamics
---

- In **spike response model(SRM)**, the neuron model is interpredted in terms of 
  - a membrane filter
  - a function describing the shape of the spike
  - a function for the time course of the threshold

- SRM is just a generalization of LIF model
- SRM has no intrinsic firing threshold but only the sharp numerical threshold for reset. Therefore, in the SRM, we work with a sharp threshold combined with a linear voltage equation.

# Definition of SRM

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/SRM.png)

1. Voltage response: $h(t) = \int_0^\infty \kappa(s)I^{\text{ext}}(t-s)ds$

1. The after-potential is described as $\eta$, then the evolution of $u$ is:

$$u(t) = \sum_f\eta(t-t^{(f)}) + \int_0^\infty\kappa(s) I^{\text{ext}}(t-s)ds + u_{rest}$$

or if we define $S(t) = \sum_f\delta(t-t^{(f)})$, then

$$u(t) = \int_0^{\infty}\eta(s)S(t-s)ds + \int_0^\infty\kappa(s) I^{\text{ext}}(t-s)ds + u_{rest}$$
- The threshold $\vartheta(t)$ is time-dependent