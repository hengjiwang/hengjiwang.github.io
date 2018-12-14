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
  Move back to HH model. For a fixed point $(u_0, w_0)$, define $\bm{x} = (u-u_0, w-w_0)^T$, then the linearization is:

  $$\frac{d\bm{x}}{dt} = \begin{bmatrix}
   F_u & F_w \\
   G_u & G_w 
  \end{bmatrix}\bm{x}$$

  where derivatives $F_u, F_w, ...$ are evaluated at the fixed point. 
  Assume $\bm{x} = C_1e^{\lambda_1t}\bm{e_1} + C_2e^{\lambda_2t}\bm{e_2}$, then the linearization can be formulated as 
  $$\lambda^2 -(F_u+G_w)\lambda +(F_uG_w - F_wG_u)=0$$
  Solve it we get $$\lambda_1+\lambda_2 = (F_u + G_w)$$ $$\lambda_1\lambda_2 = F_uG_w - F_wG_u$$.
  - **Stable:** $\lambda_1, \lambda_2 < 0$, which means $$F_u+G_w < 0 \text{ \ and \ } F_uG_w - F_wG_u>0$$
  - **Unstable:** 
    $$F_u+G_w > 0 \text{ \ and \ } F_uG_w - F_wG_u>0$$
  - **Saddle:** 
    $$F_uG_w -F_wG_u < 0$$

  Another classification is by if $\lambda_1$ and $\lambda_2$ are true real numbers, checked with the sign of $(F_u+G_w)^2 - 4(F_uG_w - F_wG_u)$:

  - **Node:** $\lambda_1$ and $\lambda_2$ are true reals$$(F_u+G_w)^2 - 4(F_uG_w - F_wG_u) > 0$$
  - **Spiral:** $\lambda_1$ and $\lambda_2$ are complex numbers$$(F_u+G_w)^2 - 4(F_uG_w - F_wG_u) < 0$$
  So put together is: 
![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/stable.png)

# 2. Type I and Type II neuron models

(to be continued...)