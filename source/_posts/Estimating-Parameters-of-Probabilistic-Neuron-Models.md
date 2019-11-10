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

For linear model

$$u(t) = \int_{0}^{\infty} \kappa(s) I(t-s)ds + u_{rest}$$

Can be approximated as

$$u_t = \sum_{l=1}^K k_lI_{t-l}dt+ u_{rest}  = {\bf{k}}\cdot{\bf{x_t}} + u_{rest}$$

Looking for its parameters is a linear regression problem. 

## 1.2 Generalized Linear Models

For SRM 

$$u(t) = \int_{0}^{\infty} \eta(s) S(t-s)ds + \int_{0}^{\infty} \kappa(s) I(t-s)ds + u_{rest}$$

we define 

$${\bf{k}} = (\kappa(dt), \kappa(2dt), \cdots, \kappa(Kdt), \eta(dt), \eta(2dt), \cdots, \eta(Jdt),u_{rest})$$

and 

$${\bf{x_t}} = (I_{t-1}dt, I_{t-2}dt, \cdots, I_{t-K}dt, n_{t-1}, n_{t-2}, \cdots, n_{t-J}, 1)$$

where $n_t \in \left\\{0,1\right\\}$ is the spike count at time $t$.

Then we obtain

$$u_t = \sum_{j=1}^J k_{K+j}n_{t-j} + \sum_{k=1}^{K} k_K I_{t-k}dt + u_{rest} = {\bf{k}\cdot x_t}$$ 

which is still a linear regression problem. 

However, spiking itself is a nonlinear process:

$$\rho(t) = f({\bf{k\cdot x_t}})$$

# 2. Statistical formulation of encoding models

We denote the observed spike train data of one neuron as $D$. For $0<t\leq T$

$$D = \left\\{n_1, n_2, ..., n_T\right\\}$$

- Neural encoding problem:
given stimulus ${\bf{x}}$, to find $p(D|{\bf{x}})$. 

Since it's not feasible to directly measure $p(D|{\bf{x}})$ for all ${\bf{x}}, D$, we actually are looking for 

$$p(D|{\bf{x}}, \theta)$$

 where $\theta =\left\\{ {\bf{k}}, b\right\\}$ is the set of model parameters. i.e. estimate $\theta$ so that the model 'fits' the observed data $D$, and then approximate

$$p(D|{\bf{x}}) \approx p(D|{\bf{x}}, \theta)$$

## 2.1 Parameter estimation

Given observed data $D$, model parameter ${\bf{k}}$ and observed stimuli $X$, there are two ways to estimate the optimized ${\bf{k}}$:

- MLE, frequencist

$${\bf{\widehat{k}}}_{MLE} = \arg\max_k p(D|X,{\bf{k}})$$

- MAP, Bayesian

$${\bf{\widehat{k}}}_{MAP} = \arg\max_k p(D|X,{\bf{k}})p({\bf{k}})$$

We assume that the spike counts per bin follow a conditional Poisson ditribution: given $\rho(t)$, $n_t \sim \text{Poiss}[\rho(t)dt]$.

Given a GLM or SRM model $\rho(t) = f({\bf{k\cdot x_t}})$, we have 

$$p(D|X,{\bf{k}}) = \prod_t \left\\{\frac{[f({\bf{k\cdot x_t}})dt]^{n_t}}{(n_t)!}\exp[-f({\bf{k\cdot x_t}})dt]\right\\}$$

take logarithm

$$\log p(D|X,{\bf{k}}) = c_0 + \sum_t \left\\{n_t\log[f({\bf{k\cdot x_t}})] - f({\bf{k\cdot x_t}})dt\right\\}$$

Two assumptions:

1. $f(u)$ is convex
2. $\log f(u)$ is concave

Then the loglikihood is concave, which means the loglikelihood has no local maximum. 

_Notice_: $D = \left\\{n_t\right\\}$ is not a Poisson process because $\rho(t)$ depends on past spikes, unless ${\bf{\eta}}=0$. 

- MAP is a penalized version of MLE

**Extend to multi-neurons spike trains:**

For the $i$-th cell:

$$\rho_i(t) = f\left({\bf{k}_i\cdot x_t} + \sum_{i'\neq i, j} \epsilon_{i',j}n_{i',t-j}\right)$$

# 3. Evaluating goodness-of-fit

## 3.1 Comparing spiking membrane potential recordings

- squared error drawbacks
  - assuming the remaining error has a Gaussian distribution
  - small jitter in the firing time of the action potential implies a large error in the membrane potential.

-- goodness-of-fit of subthreshold membrane potential should be considered separately from that of the spike times. 


![](https://raw.githubusercontent.com/hengjiwang/hengjiwang.github.io/hexo/blog_figures/RMSEnm.png)

![](https://raw.githubusercontent.com/hengjiwang/hengjiwang.github.io/hexo/blog_figures/RMSEnn.png)

$$\text{RMSER} = \frac{RMSE_{nn}}{RMSE_{nm}}$$

## 3.2 Spike train likelihood

(to be continued ... )