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
$$\tau_m \frac{du}{dt} = f(u) -R\sum_k w_k + RI(t)$$
$$\tau_k \frac{dw_k}{dt} = a_k(u-u_{rest}) - w_k + b_k\tau_k \sum_{t^{(f)}}\delta(t-t^{(f)})$$

- The $\delta$-term in the last equation indicates that during a firing, the **adaptation currents** $w_k$ are increased by an amount $b_k$

## 1.2 AdEx model
$$\tau_m \frac{du}{dt} = -(u-u_{rest}) + \Delta_T \exp(\frac{u-\vartheta_{rh}}{\Delta_T}) -Rw + RI(t)$$
$$\tau_w \frac{dw}{dt} = a_k(u-u_{rest}) - w + b\tau_w \sum_{t^{(f)}}\delta(t-t^{(f)})$$
- A single adaptive term $w$
- $a$ couples adaption to the voltage and is the source of subthreshold adaption.
- The choice of $a$ and $b$ largely determines the firing pattern of the neuron, which is based on dynamics of ion channels.

# 2. Firing patterns

**Firing patterns** from AdEx model, with different parameter set and stimulated with a step current with high/low amplitude:

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/firepattern.png)

## 2.1 Classification of firing patterns

- Initial transient
  - **tonic:** $f_{init} \approx f_{rest}$
  - **initial burst:** $f_{init} \gg f_{rest}$
  - **delay:** firing starts with a delay
- Steady state pattern
  - **tonic:** regularly spaced
  - **adapting:** increasing interspike intervals
  - **bursting:** regularly alternations between short and long intervals
  
large $\tau_w$ small $b$ $\rightarrow$ weak but long-lasting currents  $\rightarrow$ adaptation

small $\tau_w$ large $b$ $\rightarrow$ short but strong currents $\rightarrow$ tonic (with a prolongation of the refractory period)
- **facilitation:** $b<0$, the interspike interval may gradually decrease.