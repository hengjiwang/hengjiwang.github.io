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

$$\tau_{m}{{\text{d}}\over{\text{d}}t}u_{i}=-u_{i}+R\,I_{i}(t)\quad{\rm for~{}}u_{i}<\vartheta$$  

where 

$$I_{i}=\sum_{j=1}^{N}\sum_{f}w_{ij}\alpha(t-t_{j}^{(f)})+I^{\rm ext}(t)\,$$

for homogeneous network

$$I(t)=w_{0}\,N\int_{0}^{\infty}\alpha(s)\,A(t-s)\,{\text{d}}s+I^{\rm ext}(t)\,$$

## 2.2 Heterogeneous networks

If there is a strong heterogeneity in the network, then we should split the population into two populations until homogeneous groups remain.

## 2.3 Connectivity Schemes

- **scaling behavior:** a change in the number $N$ of neurons that participate in the population
  - $N$ is relative constant in adulthood for biology
  - For saving time we can simulate 20000 neurons with like 4000 neurons and a 4 times larger connection strength

### 2.3.1 Full connectivity

- **All-to-all connectivity** is the simplest coupling scheme for a population where all connections have the same strength 
  
  $$w_{ij} = \frac{J_0}{N}$$ 
  
  If $N\rightarrow \infty$ then there is no fluctuation (which is nonphysical). 
  - a more intricate version is $w_{ij}\sim \mathcal{N}(J_0/N, \sigma_0^2/N)$

### 2.3.2 Random coupling: fixed coupling probability

- fix a **connction probability $p$**, then for a postsynaptic neuron the number of presynaptic input links has a mean $\langle C_j \rangle = pN$, of which the fluctuation is $p(1-p)N$. 
- Or we can fix $C = pN$ and randomly choose $C$ presynaptic neurons for any postsynaptic neuron $j$: $C_j=C$. Then the connection strength is 

$$w_{ij} = \frac{J_0}{C} = \frac{J_0}{pN}$$

### 2.3.3 Random coupling: fixed number of presynaptic partners

- $C$ is fixed which is independent with the scaling number $N$

### 2.3.4 Balanced excitation and inhibition

- **balanced network:** a population that total amount of excitation and inhibition cancel each other. We can scale synaptic weights so as to control specifically the amount of fluctuations of the input current around zero. An appropriate choice is 

$$w_{ij}={J_{0}\over\sqrt{C}}={J_{0}\over\sqrt{pN}}\,$$

### 2.3.5 Interacting populations

- three different types: excitatory, fastspiking inhibitory, and non-fastspiking interneurons
- It is convenient to visualize the neurons as being arranged in spatially separate pools, but this is not necesssary.
- 