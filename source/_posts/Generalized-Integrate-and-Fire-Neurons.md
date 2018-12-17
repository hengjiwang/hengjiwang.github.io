---
title: Nonlinear Leaky-Integrate-and-Fire Neurons
date: 2018-12-14 17:21:27
tags:
- neurons
- dynamics
- GLIF
categories:
- neuronal dynamics
---

# 1 Thresholds in nonlinear LIF model

- **firing time $t^{(f)}$:**

$$t^{(f)}: u(t^{(f)}) = \theta_{reset} \text{ and } \frac{du(t)}{dt}|_{t=t^{(f)}} > 0$$

- general nonlinear LIF model:
$$\tau \frac{du}{dt} = f(u) + R(u)I$$
    - when $u$ reaches $\theta_{reset}$, the dynamics stops and restarts at time $t^{(f)}+\Delta^{abs}$ with initial condition $u_r$. 
    ![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/rheo.png)
    - $\theta_{reset}$ is **firing threshold**. Usually it's just a manually defined numerical value, that if $u$ reaches $\theta_{reset}$ we conclude that there is a spike and reset $u$ to $u_r$; otherwise not.

    - $\vartheta$ serves as a **critical voltage** for spike initiation by a short current pulse. It is an unstable fixed point when $I=0$, which means if $u$ reaches $\vartheta$, even if we immediately change $I$ to zero, $u$ will still keep increasing until it reaches $\theta_{reset}$.
 
    - $\vartheta_{rh}$ is **rheobase threshold** for repetive firing, where the stable fixed point disappears. $I_c = \vartheta_{rh}/R$ is called the **rheobase current**. A stationary voltage $u>\vartheta_{rh}$ is impossible. However, for pulse inputs or time-dependent currents, volatge transients into the regime $\vartheta_{rh} < u(t) < \vartheta$ routinely occur without initiating a spike. 

    ![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/phasethres.png)
  
# 2 Exponential LIF Model

$$\tau \frac{du}{dt} = -(u-u_{rest}) + \Delta_T \exp\left(\frac{u-\vartheta_{rh}}{\Delta_T}\right) + RI$$

- **leaky term:** $-(u-u_{rest})$
- **sharpness parameter:** $\Delta_T$
  
(typically the **absolute refractory time $0< \Delta^{abs}< 5ms$**)

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/expLIF.png)

- The right-hand side function when $I=0$: 
$$f(u) = -(u-u_{rest}) + \Delta_T \exp\left(\frac{u-\vartheta_{rh}}{\Delta_T}\right)$$
should satisfy $\vartheta \gg u_{rest} + \Delta_T$ so that when $u$ is around $u_{rest}$ the exponential term becomes negligiby small. 

- $\vartheta$ for this model lies a little larger than $\vartheta_{rh}$.

- If $\Delta_T \rightarrow 0$, then $\vartheta_{rh} = \vartheta$ and this model returns to a LIF model. 

- **refractory exponential integrate-and-fire model**: an exponential integrate-and-fire model where the parameters depend on the time since the last spike. 
## 2.1 How do we choose $f(u)$ in practice?

Fitting from experiments:
$$\tilde{f}(u) = \langle \frac{1}{C} I(t) - \frac{du(t)}{dt}\rangle$$
where $\tilde{f} = f/\tau, C=\tau/R$.
$I(t)$ and $\frac{du(t)}{dt}$ can be obrained from experiments, $C$ is chosen to minimize the experimental variance. 

# 3 Quadratic LIF Model

$$\tau \frac{du}{dt} = a_0 (u-u_{rest})(u-u_c) + RI$$

where $u_c > u_{rest}$ is a critical voltage for spike initiation by a short current pulse.

- This model is closely related to **$\Theta$-neuron**, a **canonical type-I model**. 
  ![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/quadrandexp.png)
- Near $\vartheta_{rh}$, the exponential LIF model and the quadratic LIF model become very similar.  

**Pros and Cons**(compared with exponential LIF model):

- **Pros:**
  - More handy for mathematiical analysis.
  
- **Cons:**
  - Worse than exponential LIF in fitting experimental data. So not suitable for predicting spike times and voltage.
  - The upswing of a spike is not rapid enough. 

- By adding an injection current, $u_r^{\text{eff}}$ and $\vartheta^{\text{eff}}$ can be very close around $\vartheta_{rh}$, thus quadratic LIF model is valid in this regime.

- Any type-I neuron model close to the bifurcation point can be approximated by a quadratic LIF model -- **canonical type-I LIF model**.

<font color='red'> Both exponential LIF and quadratic LIF models show a f-I curve of type I.