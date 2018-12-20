---
title: Adaption
date: 2018-12-16 22:29:41
tags:
- neurons
- dynamics
- GLIF
- applied math
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

**Firing patterns** from AdEx model, with different parameter set and stimulated with a <font color=red>step current</font> with high/low amplitude:

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

## 2.2 Phase Analysis of firing patterns

Each time that $u=\theta_{reset}$, it will be initialized at $(u_r, w+b)$

Tonic:

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/tonicphase.png)

Adapting:

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/adaptphase.png)

Bursting:
Alternations between short and long interspike intervals.

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/burstphase.png)

Irregular:
Comes from chaotic reset.

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/irrphase.png)

Transient:

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/transientphase.png)

## 2.3 Space of Reset Parameters

Reset parameters: $u_r, b$

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/resetphase.png)

## 2.4 Space of Subthreshold Parameters

- Exponential LIF looses stability via a saddle-point bifurcation.
- AdEx looses stability via a 
  - Hopf bifurcation: $aR>\tau_m/\tau_w$
  - saddle-node bifurcation: $aR<\tau_m/\tau_w$

-- The type of bifurcation has no influence on the <font color=red>firing pattern (by step current)</font> which depends mainly on the choice of reset parameters.
-- The subthreshold parameters do control the presence of absence of oscillations in response to a <font color=red>short pulse</font>.

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/resonator.png)

- **resonator:** a model showing damped oscillations
- **integrator:** a model without oscillations

The frequency of the damped oscillation is given by:
$$w = \frac{4}{\tau_w}\left[aR - \frac{2\tau_w}{\tau_m}\left(1-\frac{\tau_m}{\tau_w}\right)^2\right]$$

# 3. Biophysical Origin of Adaption

## 3.1 by a single slow channel
- Still model sodium channels with AdEx model.

- Consider the potassium channel of HH type:
$$\tau_m \frac{du}{dt} = -(u-E_L) - R_L g_K n^p (u-E_K) + R_L I_{ext}$$

$$\frac{dn}{dt} = -\frac{n-n_0(u)}{\tau_n(u)}$$

resting voltage $E_0$ can be analytically solved:

$$E_0 = \frac{E_L + (R_L g_K)n_0(E_0)^pE_K}{1+(R_Lg_K)n_0(E_0)^p}$$

Define $\beta = g_Kpn_0(E_0)^{p-1}(E_0-E_K)$; 
Expand $n_0(u) = n_0(E_0) + n_0'(u-E_0)$;
Define variable $w = \beta[n-n_0(E_0)]$,
then we get

$$\tau_n(E_0)\frac{dw}{dt} = a(u-E_0) - w$$

$$\tau_m^{\text{eff}}\frac{du}{dt} = -(u-E_0)- Rw+RI_{ext}$$

($R$ and $\tau_m$ rescaled)

Derivations above show that each channel gives rise to an effective adaptation variable $w$. Since there are many channels, we expect many $w_k$.

- **spike-triggered adaption:** each additional spike activate the channel further

## 3.2 by passive dendrites

$$\frac{dV^s}{dt} = \frac{1}{C^{s}}\,\left[-{(V^{s}-u_{\rm rest})\over R_{\text{T}}^{%
s}}-{V^{s}-V^{d}\over R_{\text{L}}}+I(t)\right]$$

$$\frac{dV^d}{dt} = \frac{1}{C^{d}}\,\left[-{(V^{d}-E^{d})\over R_{\text{T}}^{d}}-{V^%
{d}-V^{s}\over R_{\text{L}}}\right]$$

Define $w = -(V^{d}-u_{\rm rest})/R_{\text{L}}$;
Assume $E^d = u_{rest}= E$, 
then we get 

$$\tau^{\rm eff}{dV^{s}\over dt} = -(V^{s}-E)-R^{\rm eff}\,w$$

$$\tau_w \frac{dw}{dt} = a\,(V^{s}-E)-w$$

1. where $a=-[R_{\rm L}+(R^{2}_{\rm L}/R_{\rm D})]^{-1}$ is always negative, which means that passive dendrites introduce a facilitating subthreshold coupling.
2. when $R_L$ is small, facilitation is strong
3. timescale of the facilitation $\tau_w$ is smaller than the dendritic time constant $R^d_TC^d$, which means compared to other adaption currents, the dendritic current is a relatively fast one.

- The dynamics of spike-triggered currents on multiple timescales can be understood in terms of their stereotypical effect on the membrane potential