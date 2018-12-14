---
title: Dynamics of Single Neurons
date: 2018-12-14 00:03:20
tags:
- neurons 
- dynamics
- applied math
categories: 
- neuronal dynamics
---

# 0. Hodgkin-Huxley Model

**Hodgkin-Huxley (HH)** model is a starting point for detailed modeling and dynamics analysis of single neurons. 

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/HH.png)

$$I=C_m\frac{du}{dt}+g_Kn^4(u-E_K)+g_{Na}m^3h(u-E_{Na})+g_L(u-E_L)$$
$$\frac{dn}{dt} = \alpha_n(u)(1-n) - \beta_n(u)n$$
$$\frac{dm}{dt} = \alpha_m(u)(1-m) - \beta_m(u)m$$
$$\frac{dh}{dt} = \alpha_h(u)(1-h) - \beta_h(u)h$$
where $\alpha_p(u)$ and $\beta_p(u)$ are related to activation and inactivation rates which are derived from Bolzmann equations. 

# 1. Phase plane analysis

# 2. Type I and Type II neuron models

(to be continued...)