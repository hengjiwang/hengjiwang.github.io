---
title: Leaky-Integrate-and-Fire Neurons
date: 2018-12-13 20:58:48
tags: 
- dynamics
- neurons
categories: 
- neuronal dynamics
---

# 1 Elements of Neuronal Systems

- We will consider: spiking neurons

- We will neglect: glia cells, non-spiking neurons

## 1.1 The Ideal Spiking Neuron

- A neuron has three functional parts:
  - **dendrites:** 'input device' that collects signals from other neurons and transmit them to the soma
  - **soma:** 'cpu' that performs an non-linear processing step
  - **axon:** 'output device' that delivers the signal to other neurons

- **synapse:** the junction between two neurons 

## 1.2 Spike Trains

- Neuronal signal: short electrical **pulses** (**action potentials** or **spikes**), which is the elementary unit of signal transmission.
  -  typical amplitude: 100 mV
  -  typical duration 1-2 ms
  
- **Spike trains:** A chain of action potentials emitted by a single neuron. 
  
- What matters? 
  - The number and the timing of spikes of a spike train. 

- Spikes are separated: <font color=red>it's impossible to excite a second spike during or immediately after a first one. </font>The minimal distance between two spikes is **refractory period**. 

## 1.3 Synapses

- **chemical synapses**
  - axon $\rightarrow$ **synaptic cleft** $\rightarrow$ postsynaptic neuron

- **electrical synapses (gap junctions)**
  - not much is known


# 2 Elements of Neuronal Dynamics

## 2.1 Postsynaptic Potentials

- **PSP:** postsynaptic potential
  - **EPSP:** excitatory PSP
  - **IPSP:** inhibitory PSP
  
(* EPSP doesn't strictly indicates a spike.)

## 2.2 Firing Threshold and Action Potential

- When membrane potential of a neuron reaches a **threshold** there will be a spike. 



# 3 Leaky-Integrate-And-Fire Models (LIF)

Neuronal dynamics can be conceived as an integration process combined with a triggering-spike mechanism. 

## 3.1 Model

![Integration-And-Fire model](https://raw.githubusercontent.com/hengjiwang/hengjiwang.github.io/hexo/blog_figures/intgrate_and_fire_model.png)

$$I(t) = I_R + I_C = \frac{u(t) - u_{rest}}{R} + C\frac{du}{dt}$$
Then we get
$$RC \frac{du}{dt} = -(u(t) - u_{rest}) + RI(t)$$

 - When u(t) reaches a threshold, we will assume there is a $\delta$ pulse and then immediately reset u(t) to a value $u_r$:

![](https://raw.githubusercontent.com/hengjiwang/hengjiwang.github.io/hexo/blog_figures/LIF.png)

This turns to a time stepping problem that can be solved with python (use package **brian2** here):

```python
%matplotlib inline
import brian2 as b2
import matplotlib.pyplot as plt
import numpy as np
from neurodynex.leaky_integrate_and_fire import LIF
from neurodynex.tools import input_factory, plot_tools


LIF.getting_started()
LIF.print_default_parameters()
```

details and exercises here: [https://neuronaldynamics-exercises.readthedocs.io/en/latest/exercises/leaky-integrate-and-fire.html](https://neuronaldynamics-exercises.readthedocs.io/en/latest/exercises/leaky-integrate-and-fire.html)

## 3.2 Liminations 

LIF model is an extremely simplified model.

- No memory of previous spikes is kept.

  - cannot capture **adaption** which exhibits in **regular-firing neurons**; instead can model **fast-spiking neurons** well

  - More complex: **bursting** and **stuttering** neurons

- Shunting inhibition and reversal potential
  - **PSC(postsynaptic current):** an input current from the spikes emitted by the presynaptic neurons:
    $$\text{PSC} \propto (u_0 - E_{syn}) $$

    where $E_{syn}$ is the **reversal potential** of the synapse.
- Conductanc echanges after a spike
- Spatial Structure

## 3.3 Benefits

- LIF model works accurately when predict precisely timed events in time, which is good for spike generation _in the soma._ But some parameters may need to be tuned. e.g. threshold depends on time. 
