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