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

# 1. Definition of SRM

![](https://raw.githubusercontent.com/hengjiwang/hengjiwang.github.io/hexo/blog_figures/SRM.png)

1. Voltage response: $h(t) = \int_0^\infty \kappa(s)I^{\text{ext}}(t-s)ds$

1. The after-potential is described as $\eta$, then the evolution of $u$ is:

$$u(t) = \sum_f\eta(t-t^{(f)}) + \int_0^\infty\kappa(s) I^{\text{ext}}(t-s)ds + u_{rest}$$

or if we define $S(t) = \sum_f\delta(t-t^{(f)})$, then

$$u(t) = \int_0^{\infty}\eta(s)S(t-s)ds + \int_0^\infty\kappa(s) I^{\text{ext}}(t-s)ds + u_{rest}$$
- The threshold $\vartheta(t)$ is time-dependent

    a standard model is 
    $$\vartheta(t) = \vartheta_0 + \sum_f \theta_1(t-t^{(f)})$$
    which can be absorbed by defining 
    $$\eta(t-t^{(f)})\rightarrow \eta^{\text{eff}}(t-t^{(f)}) = \eta(t-t^{(f)})- \theta_1(t-t^{(f)})$$ 

- If we just want to predict spike times but not the membrane potential, we can integrate $\eta$ into the dynamic threshold so that $u^{\text{eff}}(t) = h(t)$

# 2. Interpretation of $\eta$ and $\kappa$

- kernel $\kappa$ is the linear response of the membrane potential to an input current.
- $\eta$ describes the standard form of an action potential of neuron i including the _negative_ overshoot which typically follows a spike (the spike afterpotential).
  - plays a role of reset:
  $$\eta(t-t^{(f)}) = -\eta_0 \exp\left(-\frac{t-t^{(f)}}{\tau_{\text{recov}}}\right)$$
- LIF model is a special case of SRM with $\eta_0=(\vartheta-u_r)$ and $\tau_{\text{recov}}= \tau_m$
- Absolute refractoriness can be incorporated in SRM by setting the dynamic threshold during $\Delta^{abs}$ to an extremely high value that cannot be attained.
- Relative _refractoriness_ can be mimicked in various ways:
  - 1. slow the recovery speed of $u$ after a spike
  - 2. a transient increase of the firing threshold (mentioned above)
  - 3. reduce the responsiveness of the neuron: making the shape of $\eta$ and $\kappa$ depend on the last spike timing $\hat{t}$:
    $$u(t) = \sum_f\eta(t-t^{(f)}) + \int_0^\infty\kappa(t-\hat{t}, s) I^{\text{ext}}(t-s)ds + u_{rest}$$

# 3. Mapping LIF to SRM

- Reconsider the "reset" in LIF
  - suppose there is a short current $I^{out}_i = -q\delta(t)$, which remove a charge $q$ from the capacitor $C$ and lower the potential by $\Delta u=-q/C = -(\vartheta-u_r)$, so the total reset current is 
  $$I^{out}_i(t) = -C(\vartheta-u_r)\sum_f\delta(t-t^{(f)}_i)$$
  - Thus the LIF model can be written as
  
  $$\tau_m \frac{du_i}{dt} = -(u_i-E_0)-R\sum_k w_k + RI_i(t) -RC(\vartheta-u_r)\sum_f\delta(t-t_i^{(f)})$$

  $$\tau_k \frac{dw_k}{dt} = a_k(u_i-E_0) - w_k + \tau_kb_k\sum_{t^{(f)}}\delta(t-t^{(f)})$$

    Integrate in the directions of eigenvectors we get

    $$u_i(t) = \sum_f \eta(t - t_i^{(f)}) + \int_0^{\infty}\kappa(s)I_i(t-s)ds$$

    with kernels

    $$\eta(s) = \sum_{k=0}^K \gamma_k {\bf{e}}_{k0}\exp(\lambda_ks)\Theta(s)$$

    $$\kappa(s) = \sum_{k=0}^K \beta_k{\bf{e}_{k0}}\exp(\lambda_ks)\Theta(s)$$

SRM is the starting point for the GLIF Models in the presence of noise.

