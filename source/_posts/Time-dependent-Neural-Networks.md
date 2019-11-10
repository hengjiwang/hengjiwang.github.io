---
title: Dynamics of Populations and Networks
date: 2019-01-05 11:27:01
tags:
- neurons
- network
- populaion
- dynamics
categories:
- neuronal dynamics
---
# 1. Continuity equation

- For $N\rightarrow\infty$, the fraction of neurons with $u_0 < u_i(t) \leq u_1$ is 

    $${n(u_{0};u_{1})\over N}=\int_{u_{0}}^{u_{1}}p(u^{\prime},t)\,{\text{d}}u^{\prime}\,.$$

    where $p(u,t)$ is **membrane potential density** for a single neuron which satisfies $\int_{-\infty}^{\theta_{\rm reset}}p(u,t)\,{\text{d}}u=1\,.$
- **flux $J(u,t)$**: the net fraction of trajectories per unit time that crosses the value $u$.
  - $NJ(u_0,t)\Delta t$ describes the number of trajectories that cross in the interval $\Delta t$ the boundary $u_0$ from below minus those from above.
- **continuity equation**: (derived from conservation of the number of trajectories)
    $$\qquad{\partial\over\partial t}p(u,t)=-{\partial\over\partial u}J(u,t)\quad{\rm~{}for~{}}u_r<u<\theta_{\text{reset}}\,$$

    generally is

    $$\qquad{\partial\over\partial t}p(u,t)=-{\partial\over\partial u}J(u,t)+A(t)\,\delta(u-u_{r})-A(t)\,\delta(u-\theta_{\rm reset})\,$$

    where the terms containing the population activity $A(t)$ represent as the source(end) of new trajectories.

    - By definition we have

    $$A(t) = J(\theta_{\rm reset}, t)$$

# 2. Stochastic spike arrival

## 2.1 Flux

For a homogeneous population, we assume that all neurons in the population receive the same driving current $I^{ext}$. In addition each neuron receives stochastic background input with jump size $w_k$ and spike arrival rate $\nu_k$ for type $k$ synapse. We seperate the flux into two contributions

$$J(u_{0},t)=J_{\rm drift}(u_{0},t)+J_{\rm jump}(u_{0},t)\,$$

where 

$$J_{\rm jump}(u_{0},t)=\sum_{k}\nu_{k}\,\int_{u_{0}-w_{k}}^{u_{0}}p(u,t)\,{\text{d}}u\,$$

denotes the flux contributed by spike arrivals.

$$J_{\rm drift}(u_{0},t)=\left.{\text{d}u\over{\text{d}}t}\right|_{u_{0}}p(u_{0},t)={1\over\tau_{m}}\,[f(u_{0})+R\,I^{\rm ext}(t)]\,p(u_{0},t)\,$$

denotes the flux contributed by the finite input current $I^{\rm ext}$

## 2.2 Population activity

- total flux at the threshold (population activity)

    $$A(t)={1\over\tau_{m}}\,[f(\theta_{\rm reset})+R\,I^{\rm ext}(t)]\,p(\theta_{\rm reset},t)+\sum_{k}\nu_{k}\,\int_{\theta_{\rm reset}-w_{k}}^{\theta_{\rm reset}}p(u,t)\,{\text{d}}u\,$$

- population density (insert $J_{\rm jump}, J_{\rm drift}$ to the continuity equation)

    $$\displaystyle{\partial\over\partial t}p(u,t) = \displaystyle-{1\over\tau_{m}}\,{\partial\over\partial u}\left(\left[f(u)+R\,I^{\rm ext}(t)\right]\,p(u,t)\right)$$

    $$\displaystyle+\sum_{k}\nu_{k}(t)\,\left[p(u-w_{k},t)-p(u,t)\right]$$

    $$\displaystyle+A(t)\,\delta(u-u_{r})-A(t)\,\delta(u-\theta_{\rm reset})\,$$

- the dynamics of $p(u,t)$ in a population of LIF neurons is nearly identical to that of a single LIF neuron _with stochastic spike arrival_.

# 3. Fokker-Planck equation

_valid condition_: neurons in the population receive many inputs that each cause a small change of the membrane potential.

- **Fokker-plank equation** is a Tylar expansion form of the population density equation of last section:

$$\tau_m\displaystyle{\partial\over\partial t}p(u,t) = \displaystyle-{\partial\over\partial u}\left(\left[f(u)+R\,I^{\rm ext}(t)+\tau_{m}\sum_{k}\nu_{k}(t)\,w_{k}\right]\,p(u,t)\right)$$

$$\displaystyle+{1\over 2}\,\left[\tau_{m}\sum_{k}\nu_{k}(t)\,w_{k}^{2}\right]\,{\partial^{2}\over\partial u^{2}}p(u,t)$$

$$\displaystyle+\tau_{m}\,A(t)\,\delta(u-u_{r})-\tau_{m}\,A(t)\,\delta(u-\theta_{\rm reset})+{\mathcal{O}}(\omega_{k}^{3})\,.$$

it can be described in three parts:

1. The total 'drive' in voltage units

$$\mu(t)=R\,I^{\rm ext}(t)+\tau_{m}\sum_{k}\nu_{k}(t)\,w_{k}$$

2. The amount of diffusive noise

$$\sigma^{2}(t)=\tau_{m}\sum_{k}\nu_{k}(t)\,w_{k}^{2}\,$$

3. The firing threshold acts as an absorbing boundary so that the density at threshold vanishes:

$$p(\theta_{\rm reset},t)=0\,$$

Insert the noise and do integration at $\theta_{reset}$ then we get

$$A(t)={\sigma^{2}(t)\over 2\tau_{m}}{\partial p(u=\theta_{\rm reset},t)\over\partial u}\,$$

# 4. Networks of LIF neurons

## 4.1 Multiple populations

Consider $K$ populations where population $k$ contains $N_k$ neurons and its activity is $A_k$. Then the number of spikes emitted by population $k$ in $\Delta t$ is $N_kA_k(t)\Delta t$. 

Suppose population $k$ send spikes to population $n$, then the spike arrival rate from population $k$ to $n$ is $\nu_k(t) = N_kA_k(t)$ (fully connectivity) or $\nu_{k}(t)=C_{nk}\,A_{k}(t)$(random connectivity with a connection probability $p_{nk}=C_{nk}/N_{k}$). Assume all connections have the same weight $w_{nk}$.

- The Fokker-Planck equation for population $n$ in the network with LIF neurons is 

    $$\displaystyle\tau_{n}{\partial\over\partial t}p_{n}(u,t) = \displaystyle-{\partial\over\partial u}\left(\left[-u+R_{n}\,I_{n}^{\rm ext}(t)+\tau_{n}\sum_{k}C_{nk}A_{k}(t)\,w_{nk}\right]\,p_{n}(u,t)\right)$$

    $$\displaystyle+{1\over 2}\,\left[\tau_{n}\sum_{k}C_{nk}A_{k}(t)\,w_{nk}^{2}\right]\,{\partial^{2}\over\partial u^{2}}p_{n}(u,t)$$

    $$\displaystyle+\tau_{n}\,A_{n}(t)\,\delta(u-u_{r}^{n})-\tau_{n}\,A_{n}(t)\,\delta(u-\vartheta_{n})\,$$

- Population activity is 

    $$A_{n}(t)=-{1\over 2}\,\left[\sum_{k}C_{nk}A_{k}(t)\,w_{nk}^{2}\right]\,{\left({\partial p_{n}(u=\vartheta_{n},t)\over\partial u}\right)}\,$$

- Diffusive noise:

    $$\sigma_{n}^{2}(t)=\tau_{n}\,\left[\sum_{k}C_{nk}A_{k}(t)\,w_{nk}^{2}\right]\propto 1/N_k\,$$

Some times it's useful to focus a single population and treat the input from other populations as background input. 

## 4.2 Synchrony, oscillations and irregularity

Suppose a network with two populations: a population of $N_E$ excitatory neurons coupled to a population with $N_I=N_E/4$ inhibitory neurons. There are $C_E$ connections from $E$ to $I$ and $C_I = C_E/4$ connections from $I$ to $E$. Weights are $w_{EE}=w_{IE}=w_{0}$ and $w_{EI}=w_{II}=-g\,w_{0}$.

- Four states of a population:
  - **asynchronous irregular (AI):** fire at different times and the distribution of interspike intervals is fairly broad 
    - it corresponds to the stationary activity
  - **synchronous rregular (SR):** periodic oscillations of the population activity and a sharply peaked interval distribution of individual neurons
  - **synchronous irregular (SI)**
    - **SI fast**
    - **SI slow**

![](https://github.com/hengjiwang/hengjiwang.github.io/blob/hexo/blog_figures/syn.png)

# 5. Networks of nonlinear LIF neurons

In a stationary state, the continuity equation becomes 

$${\partial\over\partial u}J(u,t)=A(t)\,\delta(u-u_{r})-A(t)\,\delta(u-\theta_{\rm reset})\,$$

...

# 6. Neuronal adaption and synaptic conductance

Consider a network consisting of $K$ populations. The dynamics of neuron $i$ in the network with adaption is 

$$\tau_m \frac{du_i}{dt} = \displaystyle f(u_{i})-R\,\sum_{k}w_{k,i}+R\,I_{i}(t)$$

$$\tau_k \frac{dw_{k,i}}{dt} = \displaystyle a_{k}\,(u-u_{\rm rest})-w_{k,i}+{b_{k}\tau_{k}}\sum_{t^{(f)}}\delta(t-t_{i}^{(f)})\,$$

where $f(u)=-(u-u_{\rm rest})+{\Delta_{T}}\,\exp\left({u-\vartheta_{rh}\over\Delta_{T}}\right)$ and 

$$I_{i}(t)=\sum_{j}\sum_{f}g_{ij}(t-t_{j}^{(f)})\,(u_{i}-E_{ij}^{\rm syn})\,$$

where $j$ denotes other neurons.

## 6.1 Adaptation currents

Consider a AdEx model and drop the index $i$, with a stochastic spike arrival $\mu(t) + \xi(t)$ where $\mu(t)=R\,\langle I(t)\rangle$

$$\tau_m \frac{du}{dt} = \displaystyle-(u-u_{\rm rest})+{\Delta_{T}}\,\exp\left({u-\vartheta_{rh}\over\Delta_{T}}\right)-R\,w+\mu(t)+\xi(t)$$

$$\tau_w \frac{dw}{dt} = \displaystyle a\,(u-u_{\rm rest})-w+{b\tau_{w}}\sum_{t^{(f)}}\delta(t-t^{(f)})$$

## 6.2 Embedding in a network

1. Determine the stationary state $A_0$ self-consistently -- use $g_\sigma(I_0)$ where $I_0 = \mu/R$ and $\sigma$ depend on $A_0$

2. Determine modulations $\hat{G}_\mu (\omega)$ and $\hat{G}_\sigma(\omega)$

3. Use the inverse Fourier transform to find $G_\mu(s)$ and $G_\sigma(s)$, then we get 

    $$A(t)=A_{0}+\int_{0}^{\infty}G_{\mu}(s)\,\Delta I(t-s)\,{\text{d}}s+\int_{0}^{\infty}G_{\sigma}(s)\,\Delta\sigma(t-s)\,{\text{d}}s\,$$

4. Use the fact that both $I(t)$ and $\sigma(t)$ are propotional to $A(t)$:

    $$\Delta A(t)=\int_{0}^{\infty}[J_{\mu}\,G_{\mu}(s)+J_{\sigma}\,G_{\sigma}(s)]\,\Delta A(t-s)\,{\text{d}}s$$

5. Search for solutions $\Delta A(t)=\epsilon\,\exp[\lambda(\omega)t]\cos(\omega t)$. If there exists a frequency for which $\lambda(\omega)>0$ then the stationary state of asynchronous firing with activity $A_0$ is unstable. 

## 6.3 Conductance input vs. current input

- conductance input is more accurate
    $$I_{i}(t)=\sum_{j}\sum_{f}w_{ij}g_{ij}(t-t_{j}^{(f)})\,(u_{i}(t)-E_{\rm syn})$$

For a homogeneous population with $N_E$ excitatory and $N_I$ inhibitory LIF neurons in the subthreshold regime

$$C{\text{d}u\over{\text{d}}t}=-g_{L}\,(u-E_{L})-g_{E}(t)\,(u-E_{E})-g_{I}(t)\,(u-E_{I})$$

We assume 

$$g_{E}(t)=\Delta g_{E}\,\sum_{j}\sum_{f}\exp[-(t-t_{j}^{(f)})/\tau_{E}]{\mathcal{H}}(t-t_{j}^{(f)})$$

For spike arrival rates $\nu_E, \nu_I$, the mean excitatory conductance is 

$$g_{E,0}=\Delta g_{E}\,\nu_{E}\,\tau_{E}\,$$

The variance of conductance is 

$$\sigma_{E}^{2}=0.5(\Delta g_{E})^{2}\,\nu_{E}\,\tau_{E}$$

Define $g_{E,f}(t)=g_{E}(t)-g_{E,0}$, then

$$C{\text{d}u\over{\text{d}}t}=-g_{0}\,(u-\mu)-g_{E,f}(t)\,(u-E_{E})-g_{I,f}(t%
)(u-E_{I})$$

where $g_{0}=g_{L}+g_{E,0}+g_{I,0}$ and $\mu={g_{L}\,E_{L}+g_{E,0}\,E_{E}+g_{I,0}\,E_{I}\over g_{0}}\,.$

The **effective membrane time constant** is 

$$\tau_{\rm eff}={C\over g_{0}}={C\over g_{L}+g_{E,0}+g_{I,0}}$$

The fluctuating part of the dynamics equation can be approximated as 

$$g_{E,f}(t)\,(u-E_{E})=g_{E,f}(t)\,(\mu-E_{E})+g_{E,f}(t)\,(u-\mu)$$

$$\approx g_{E,f}(t)\,(\mu-E_{E})$$

which doesn't depend on $u(t)$ and can be regarded as the summed effects of postsynaptic current pulses. So *in the stationary state, a conductance-based synapse model is well approximated by a current-based model of synaptic input.*

## 6.4 Colored noise

White-noise approximation is valid only when $\tau_E$ and $\tau_I$ is short. If they are slow then the fluctuations of inputs will have temporal correlations, and a colored noise should be considered. 

A mean input to a neuron $i$ in population $n$ from population $k$ is

$$I_{i}(t)=\sum_{k}C_{nk}w_{nk}\int_{0}^{\infty}\alpha_{nk}(s)\,A(t-s)\,{\text{d}}s\,$$

just focus on one single population coupled to itself and suppose $\alpha(s)=(q/\tau_{q})\,\exp(-s/\tau_{q})$, insert it to the above equation we have 

$${\text{d}I_{i}\over{\text{d}}t}=-{I_{i}\over\tau_{q}}+C_{nn}\,w_{nn}{q\over\tau_{q}}\,A_{n}(t)$$

where $A_n(t) = \mu(t) + \xi_i(t)$

Combined with

$$\tau_{m}\,\frac{\text{d}u_{i}}{\text{d}t}=f(u_{i})+R\,I_{i}(t)\,$$

and the rest condition -- if $u=θ_{reset}$ then $u=u_r$. Since we now have two coupled differential equations, the momentary state of a population of $N$ neurons is described by a two-dimensional density $p(u,I)$.








