---
title: Adaption
date: 2018-12-16 22:29:41
tags:
- neurons
- dynamics
- GLIF
categories:
- neuronal dynamics
---

# 1. Adaptive Exponential (AdEx) LIF model

## 1.1 Add adaptive terms
$$\tau_m \frac{du}{dt} = f(u) -R\sum_k w_k + RI(t)\\
\tau_k \frac{dw_k}{dt} = a_k(u-u_{rest}) - w_k + b_k\tau_k \sum_{t^{(f)}}\delta(t-t^{(f)})$$

- The $\delta$-term in the last equation indicates that during a firing, the **adaptation currents** $w_k$ are increased by an amount $b_k$

## 1.2 AdEx model
$$\tau_m \frac{du}{dt} = -(u-u_{rest}) + \Delta_T \exp(\frac{u-\vartheta_{rh}}{\Delta_T}) -Rw + RI(t)\\
\tau_w \frac{dw}{dt} = a_k(u-u_{rest}) - w + b\tau_w \sum_{t^{(f)}}\delta(t-t^{(f)})$$
- A single adaptive term $w$
- $a$ couples adaption to the voltage and is the source of subthreshold adaption.
- The choice of $b$ largely determines the firing pattern of the neuron, which is based on dynamics of ion channels.

# 2. Firing patterns

**Firing patterns** from AdEx model, with different parameter set and stimulated with a step current with high/low amplitude:

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/firepattern.png)