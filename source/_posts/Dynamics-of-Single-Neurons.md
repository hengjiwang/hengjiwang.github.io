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


-- _God said: Let there be spikes: and there was Hodgkin-Huxley model._

- **Hodgkin-Huxley (HH)** model is a starting point for detailed modeling and dynamics analysis of single neurons. 

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/HH.png)

$$I=C_m\frac{du}{dt}+g_Kn^4(u-E_K)+g_{Na}m^3h(u-E_{Na})+g_L(u-E_L)$$
$$\frac{dn}{dt} = \alpha_n(u)(1-n) - \beta_n(u)n$$
$$\frac{dm}{dt} = \alpha_m(u)(1-m) - \beta_m(u)m$$
$$\frac{dh}{dt} = \alpha_h(u)(1-h) - \beta_h(u)h$$
where $\alpha_p(u)$ and $\beta_p(u)$ are related to activation and inactivation rates which are derived from Bolzmann equations (details in [https://en.wikipedia.org/wiki/Hodgkin%E2%80%93Huxley_model](https://en.wikipedia.org/wiki/Hodgkin%E2%80%93Huxley_model))

# 1. Phase plane analysis

-- _we as humans prefer analyzing eveything in 2D_

## 1.1 Reduction to 2D

- The four-dimensional HH model can be reduced to a two-dimensional model (details in [T. B. Kepler (1992)](https://link.springer.com/article/10.1007/BF00197717)):

$$\frac{du}{dt} = \frac{1}{\tau}[F(u,w) + RI]$$
$$\frac{dw}{dt} = \frac{1}{\tau_w}G(u,w)$$

of which dynamics can be analyzed in a 2D phase plane.

## 1.2 Phase plane analysis

- **Nullclines:** On the phase cline, the set of points with $\dot{u}=0$ ($\dot{w}=0$) is called the u-nullcline (w-nullcline). The direction of flow on the u-nullcline (w-nullcline) is $(0, \dot{w})^T$ ($(0, \dot{u})^T$).

- **Fixed point:** The points in the phase plane with $\dot{u} = \dot{w} = 0$, which is the intersection of u-nullcline and w-nullcline. 

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/phaseplane.png)

- **Stability of Fixed points**
  Move back to HH model. For a fixed point $(u_0, w_0)$, define $\bf{x} = (u-u_0, w-w_0)^T$, then the linearization is:

  $$\frac{d\bf{x}}{dt} = \left(\begin{matrix}
   F_u & F_w\\\ 
   G_u & G_w 
  \end{matrix}\right)\bf{x}$$

  where derivatives $F_u, F_w, ...$ are evaluated at the fixed point. 
  Assume $\bf{x} = C_1e^{\lambda_1t}\bf{e_1} + C_2e^{\lambda_2t}\bf{e_2}$, then the linearization can be formulated as 
  $$\lambda^2 -(F_u+G_w)\lambda +(F_uG_w - F_wG_u)=0$$
  Solve it we get $$\lambda_1+\lambda_2 = (F_u + G_w)$$ $$\lambda_1\lambda_2 = F_uG_w - F_wG_u$$
  - **Stable:** $\lambda_1, \lambda_2 < 0$, which means $$F_u+G_w < 0 \text{  and  } F_uG_w - F_wG_u>0$$
  - **Unstable:** 
    $$F_u+G_w > 0 \text{  and  } F_uG_w - F_wG_u>0$$
  - **Saddle:** 
    $$F_uG_w -F_wG_u < 0$$

  Another classification is based on whether $\lambda_1$ and $\lambda_2$ are pure real numbers, determined by the sign of $(F_u+G_w)^2 - 4(F_uG_w - F_wG_u)$:

  - **Node:** $\lambda_1$ and $\lambda_2$ are pure reals$$(F_u+G_w)^2 - 4(F_uG_w - F_wG_u) > 0$$
  - **Spiral:** $\lambda_1$ and $\lambda_2$ are complex numbers$$(F_u+G_w)^2 - 4(F_uG_w - F_wG_u) < 0$$
  So put together all it's: 
![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/stable.png)

# 2. Type I and Type II neuron models

-- _emergence in single neurons_
- **Type I**: neurons with a continuous frequency-current curve(**f-I curve**, **gain function**).
- **Type II**: neurons with a discontinuous f-I curve. 

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/type12.png)

- **Rheobase current ($I_\theta$)**: the minimal constant current injection which triggers a repetive firing of neurons. In phase plane, it is called **bifurcation point** and $I$ is the **bifurcation parameter**.

## 2.1 Type I models
![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/typeI.png)



In this case, when $I=I_\theta$, the stable fixed point and the saddle point in A. merge into one point, at which the frequency is zero. If $I$ is higher a limit cycle will appear from zero frequency. Such transition at $I_\theta$ is called **Saddle-Node-onto-Limit-Cycle Bifurcation**.

## 2.2 Type II models

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/typeII.png)

In this case, the limit cycle appears before a saddle-node bifurcation forms thus when $I=I_\theta$ and a bifurcation point is reached, the limit cylce already has some frequency. This is called **Saddle-Node-off-Limit-Cycle Bifurcation**.

(Figures above are of reduced HH model) 

## 2.3 Hopf Bifurcation

- **Hopf bifurcation:** a scenario where there is a stability loss in combination with an emerging **oscillation**(eigenvalues are pure imaginary numbers). 

  - **Subcritical Hopf-bifurcation:** 
    - the emerged oscillatory solution at the Hopf Bifurcation point is unstable. 
    - large-amplitude oscillations close to the bifurcation point

  - **Supercritical Hopf-bifurcation:** 
    - the emerged oscillation solution at the Hopf Bifurcation point is stable. 
    - small-amplitude oscillations close to the bifurcation point
    - <font color=red>subthreshold oscillations, so not linked to neuronal firing.</font>

    Conclusion: Subcritical Hopf bifurcation exhibit a gain function of type II.

# 3. Threshold and excitability

-- _how a spike appears?_

- **Excitable systems:** _For weak stimuli, the voltage trace returns more or less directly to the resting potentials. For stronger stimuli it makes a large detour, that is, the model emits a spike._

**Type I:**

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/type1exc.png)

For input currents which are just above threshold, the action potential occurs, however, with an extremely long delay.

**Hopf-bifurcation:**

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/hopfexc.png)

Hyperpolarization appears.

**with slower $w$ dynamics...**

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/slowerw.png)

A plateau appears because of the low dynamics of $w$.
We can say in this case the model has been reduced to 1D. 