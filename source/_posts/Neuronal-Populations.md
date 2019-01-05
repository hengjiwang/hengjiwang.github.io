---
title: Neuronal Populations
date: 2018-12-31 22:54:49
tags:
- neurons
- populations
- dynamics
categories:
- neuronal dynamics
---
# 1. Columnar organization

- Neighboring neurons in the _visual cortex_ have similar **receptive fields** (similar prefered orientations)
- In _auditory cortex_, each neuron has its preferred tone frequency.
- Receptive fields also used in retinal ganglion cells, thelamic cells, olfractory cells or insect sensory systems
- **Cortical maps** -- the exact characteristics of the receptive ﬁelds change slightly as one moves parallel to the cortical surface.
- All neurons in the same column (with similar intrinsic properties) can be considered as a single population of neurons.
- Localized populations of neurons can be grouped together into populations. However a population does not require neurons need to form local groups but can distribute in different areas.

# 2. Identical neurons

- **population activity:**

$$A(t)={\rm lim}_{\Delta t\to 0}\,{1\over\Delta t}\,{n_{\rm act}(t;t+\Delta t)\over N}={1\over N}\sum_{j=1}^{N}\sum_{f}\delta(t-t_{j}^{(f)})\,$$

- Requirements:
  - large populations
  - homogeneeous populations

## 2.1 Homogeneous networks

- homogeneous:
  - all neurons $1 \leq i \leq N$ are identical
  - all neurons receive the same external input
  - the interaction strength $w_{ij}$ for the connections is **statistically uniform**: $w_{ij} \approx w_0$
    - $w_0 = 0:$ independent 
    - $w_0 < 0:$ inhibitory
    - $w_0 > 0:$ excitatory

- Homogeneous population of LIF neurons:

$$\tau_{m}{\text{d}\over{\text{d}}t}u_{i}=-u_{i}+R\,I_{i}(t)\quad{\rm for~{}}u_{i}<\vartheta$$  

where 

$$I_{i}=\sum_{j=1}^{N}\sum_{f}w_{ij}\alpha(t-t_{j}^{(f)})+I^{\rm ext}(t)\,$$

for homogeneous network

$$I(t)=w_{0}\,N\int_{0}^{\infty}\alpha(s)\,A(t-s)\,{\text{d}}s+I^{\rm ext}(t)\,$$

## 2.2 Heterogeneous networks

If there is a strong heterogeneity in the network, then we should split the population into two populations until homogeneous groups remain.

# 3. Connectivity Schemes

- **scaling behavior:** a change in the number $N$ of neurons that participate in the population
  - $N$ is relative constant in adulthood for biology
  - For saving time we can simulate 20000 neurons with like 4000 neurons and a 4 times larger connection strength

## 3.1 Full connectivity

- **All-to-all connectivity** is the simplest coupling scheme for a population where all connections have the same strength 
  
  $$w_{ij} = \frac{J_0}{N}$$ 
  
  If $N\rightarrow \infty$ then there is no fluctuation (which is nonphysical). 
  - a more intricate version is $w_{ij}\sim \mathcal{N}(J_0/N, \sigma_0^2/N)$

## 3.2 Random coupling: fixed coupling probability

- fix a **connction probability $p$**, then for a postsynaptic neuron the number of presynaptic input links has a mean $\langle C_j \rangle = pN$, of which the fluctuation is $p(1-p)N$. 
- Or we can fix $C = pN$ and randomly choose $C$ presynaptic neurons for any postsynaptic neuron $j$: $C_j=C$. Then the connection strength is 

$$w_{ij} = \frac{J_0}{C} = \frac{J_0}{pN}$$

## 3.3 Random coupling: fixed number of presynaptic partners

- $C$ is fixed which is independent with the scaling number $N$

## 3.4 Balanced excitation and inhibition

- **balanced network:** a population that total amount of excitation and inhibition cancel each other. We can scale synaptic weights so as to control specifically the amount of fluctuations of the input current around zero. An appropriate choice is 

$$w_{ij}={J_{0}\over\sqrt{C}}={J_{0}\over\sqrt{pN}}\,$$

## 3.5 Interacting populations

- Three different types: excitatory, fastspiking inhibitory, and non-fastspiking interneurons
- It is convenient to visualize the neurons as being arranged in spatially separate pools, but this is not necesssary.
- The activity of neurons in pool $n$ is 

$$A_n(t) = \frac{1}{N_n}\sum_{j\in \Gamma_n}\sum_f \delta(t-t_j^{(f)})$$

# 4. Population activity

 If we are only interested in the stationary activity in a network of neurons without worrying about the temporal aspects of population activity, then f-I curve is enough. 

- **Asynchronous firing**: a macroscopic firing state with constant activity $A(t) = A_0$, which can be derived by the gain function $g(I_0)$ of a single neuron and a coupling parameter $J_0$.

## 4.1 Stationary activity as single-neuron firing rate

For a homogeneous network with $N\rightarrow \infty$

$$A_0 := \frac{N^{sp}}{NT} = \nu_i$$

where $\nu_i$ is the firing rate of a single neuron $i$

For a finite $N$, $\langle A_0 \rangle = \nu_i$, where 

$$\nu_i = g_\sigma (I_0)$$

where a $\sigma$ denotes the existence of noise; in the absence of noise $\sigma=0$

- Notations of population activity
  - $A(t)$: direct experimental/simulational result
  - $\langle A(t) \rangle$: theoretical result
  - $\bar{A}(t)$: filtered population activity from expirical measurements in a simulation or experiment

## 4.2 Activity of a fully connected network

For a stationary population, $\int_{0}^{\infty}\alpha(s)\,A(t-s)\,{\text{d}}s=A_{0}$, so

$$I_0 = w_0 N A_0 + I_0^{\text{ext}}$$

together with $A_0 = g_0(I_0)$ and $J_0 = w_0N$ we have 

$$A_0 = g_0(J_0 A_0+I_0^{\text{ext}})$$

which means we can calculate out $A_0$ if we know $J_0$ and $g_0$

![](https://raw.githubusercontent.com/hengjiwang/blog_figures/master/graphA.png)

## 4.3 Acticity of a randomly connected network

 If all neurons fire at a rate $\nu$ then the mean input current to neuron $i$ generated by its $C_{pre}$ presynaptic partners is

 $$\langle I_0 \rangle = C_{pre}q w \nu + I_0^{\text{ext}}$$

 where $q = \int_{-\infty}^{\infty}\alpha(s)ds$ can be interpreted as the total electric charge delivered by a single input spike.

 The fluctuation is 

 $$\sigma^2_{I} = C_{pre}w^2 q_2 \nu$$

 where $q_2 = \int_{-\infty}^{\infty} \alpha^2(s) ds$

 Insert above $I_0, \sigma_I$ into the gain function $\nu = g_\sigma(I_0)$ then we get the (theoretical) mean population activity $\langle A_0 \rangle = \nu$.

 Above results are valid for any specific neuron model.

- **Brunel network: excitatory and inhibitory populations**

Suppose an excitatory population with $N_E$ neurons and an inhibitory population with $N_I$ neurons following LIF model with the same parameters $\vartheta, \tau_m, R, u_r$. Each neuron receives $C_E$ synapses from excitatory neurons with $w_E > 0$ and $C_I$ synapses from inhibitory neurons with $w_I < 0$. An excitatory presynaptic neuron contributes $\Delta u_E = w_E qR/\tau_m$ and an inhibitory one contributes $\Delta u_I = \Delta u_E w_I/w_E$. 

Define

$$\gamma={C_{I}\over C_{E}}\quad\text{ and }\quad g=-{w_{I}\over w_{E}}=-{\Delta u_{I}\over\Delta u_{E}}\,$$

Then the total input current is 

$$I_0 = \displaystyle I^{\rm ext}+q\,\sum_{j}\nu_{j}\,w_{j} = I_{0}^{\rm ext}+q\,\nu\,w_{E}\,C_{E}\,[1-\gamma\,g]\,$$

The variance is 

$$\sigma^2 = \displaystyle\sum_{j}\nu_{j}\,\tau\,(\Delta u_{j}^{2}) = \displaystyle\nu\,(\Delta u_{E})^{2}\,C_{E}\,[1+\gamma\,g^{2}]\,$$

The stationary firing rate is 

$$A_{0}=\nu=g_{\sigma}(I_{0})={1\over\tau_{m}}\left\{\sqrt{\pi}\int_{u_{r}-RI_{0}\over\sigma}^{\vartheta-RI_{0}\over\sigma}\,\exp\left({x}^{2}\right)\,\left[1+{\rm erf}(x)\right]\,\text{d}x\right\}^{-1}\,$$