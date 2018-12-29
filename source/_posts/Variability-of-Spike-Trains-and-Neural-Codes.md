---
title: Statistics of Spike Trains and Neural Encoding
date: 2018-12-25 14:02:30
tags:
- statistics
- applied math
- neurons
- data analysis
---

- *vivo* recordings of neuronal activity show a high degree of irregularity.
- *vitro* neurons/vivo neurons driven by a strong time-dependent signal show regularity.
- Irregular spontaneous activity and trial-to-trial variations in neuronal responses are often considered as **noises**. 

# 1. Spike train variability

- Neurons driven by constant stimuli show more irregularity than those driven by stimuli with high-amplitude fluctuations. 
  - Intrinsic neuronal-level noises show in *vitro*.
  - Extrinsic noises that arise from network effects occur in *vivo*.
  
## 1.1 Noise from neurons

**Intrinsic noise** sources:

1. thermal noise: $\langle\Delta u^2\rangle \propto RkTB$  
2. finite ion channels -- small fluctuations near the threshold can generate different results of spiking.

## 1.2 Noise from network

**Extrinsic noise** sources:

1. signal transmission failures
2. random connectivity of excitatory and inhibitory neurons

# 2. Mean Firing Rate    

## 2.1 Rate as a spike count

- **temporal average** firing rate in trial $k$:

$$\nu_k = \frac{n_k^{sp}}{T}$$

where $n_k^{sp}$ is the spike count, $T$ is the interval of duration.

- **Fano factor** which denotes the variance of the spike count:

$$F = \frac{\langle (\Delta n^{sp})^2)\rangle}{\langle n^{sp}\rangle}$$

where brackets denote the average over trails.

- **mean interval** between two subsequent spikes is $\frac{T}{\langle n^{sp} \rangle}$

    - For a Poisson process, $F = 1$ 
  -- thus Fano factor is a judgement criteria of whether neuronal firing is Poisson-like. 

## 2.2 Rate as a spike density

- Neuronal response of several repeated trials with the same stimulation is reported in a **Peri-Stimulus-Time Histogram(PSTH)**.
- For a bin width $\Delta t$ in PSTH, the spike density over $K$ repetitions is 

$$\rho(t) = \frac{1}{\Delta t}\frac{n_K(t;t+\Delta t)}{K}$$

in unites of Hz. 

- An **instantaneous firing rate** is 

$$\nu(t) = \langle S(t) \rangle = \langle \sum_f \delta(t-t^{(f)}) \rangle$$

- **Empirical instantaneous firing rate** is 

$$\widehat{\nu(t)} = \frac{1}{K\Delta t} \sum_{k=1}^K n_{k}^{sp} (t)$$

where $\Delta t$ is small. 

## 2.3 Rates as a population activity

- For a population with $N$ neurons (size is $N$), the **population activity** is 

$$A(t) = \frac{1}{\Delta t} \frac{n_{act}(t;t+\Delta t)}{N} = \frac{1}{\Delta t}\frac{\int_t^{t+\Delta t}\sum_j\sum_f \delta(t-t_j^{(f)})dt}{N}$$

# 3. Interval distributioin

- The **interspike interval (ISI)** distribution can be interpreted as a conditional probability density

$$P_0(s) = P(t^{(f)} + s | t^{(f)})$$

  It describes the probability (density) that the _next_ spike occurs at $t^{(f)}+s$, if there is a spike at $t^{(f)}$  

- **mean interval**

$$\langle s\rangle = \int_0^{\infty} sP_0(s)ds$$

- **mean firing rate**

$$\nu = \frac{1}{\langle s \rangle} = \left[\int_0^{\infty} sP_0(s)ds\right]^{-1}$$

- **coefficient of variation**

$$C_V^2 = \frac{\langle \Delta s^2\rangle}{\langle s\rangle^2}$$

where $\langle \Delta s^2 \rangle = \int_0^{\infty} s^2 P_0(s)ds - \langle s\rangle^2$

For a Poisson process, $C_V = 1$. 

- **autocorrelation function**

For a neuron $i$, 
$$C_{ii}(s) = \langle S_i(t) S_i(t+s)\rangle_t$$

where $\langle\cdot\rangle_t$ denotes an average over time $t$. 
  
- Different between $P_0(s)$ and $C(s)$
  - $P_0(s)$ describes the probability of the _next_ spike
  - $C(s)$ describes the probability of _another_ spike (maybe not the next)

- **power spectrum (noise spectrum)**

$$\mathcal{P}_T (w) = \frac{1}{T}\left|\int_{-T/2}^{T/2} S_i(t) e^{-iwt}dt\right|^2$$

$$\mathcal{P}(w) = \lim_{T\rightarrow\infty} \mathcal{P}_T(w)$$

The power spectrum $\mathcal{P}(w)$ of a spike train is equal to the Fourier transform of $C_{ii}(s)$

$$\hat{C}_{ii}(w) = \int_{-\infty}^{\infty} \langle S_i(t)S_i(t+s)\rangle_t e^{-iws}ds$$

$$=\lim_{T\rightarrow \infty}\frac{1}{T}\left|\int_{-T/2}^{T/2} S_i(t)e^{-iwt}dt\right|^2 = \mathcal{P}(w)$$

# 4. Renewal statistics

- Spikes are generated in a **renewal process** (only keeps a memory of the last event).
  - Poisson process with an absolute refractoriness is the simplest renewal system. 

The aim of renewal theory is to predict the probability of the next event given the age of the system:

$$P_0(s) = P(t^{(f)} + s|t^{(f)})$$

- Since the dependence of spikes is restricted to the most recent event, intervals between subsequent events are independent. 

## 4.1 Survivor function and hazard

- **survivor function** is the probability that the neuron stays quiescent between $\hat{t}$ and $t$

$$S(t|\hat{t}) = 1 - \int_{\hat{t}}^t P(t'|\hat{t})dt'$$

- **hazard (age-dependent death rate)** (rate of decay of $S(t|\hat{t})$) is 

$$\rho(t|\hat{t}) = -\frac{\frac{d}{dt}S(t|\hat{t})}{S(t|\hat{t})} = \frac{P(t|\hat{t})}{1 - \int_{\hat{t}}^t P(t'|\hat{t})dt'}$$

Solve it we get

$$S(t|\hat{t}) = \exp\left[-\int_{\hat{t}}^t \rho(t'|\hat{t})dt'\right]$$

and the explicit interval distribution

$$P(t|\hat{t}) = S(t|\hat{t})\rho(t|\hat{t}) = \rho(t|\hat{t})\exp\left[-\int_{\hat{t}}^t \rho(t'|\hat{t})dt'\right]$$

which can be interpreted as: **survive until $t$ $\times$** **fire at $t$**

- each of $\rho(t|\hat{t}), P(t|\hat{t}), S(t|\hat{t})$ is sufficient to describe a renewal system. 

## 4.2 Renewal theory

- Renewal theory is associated with **stationary input** conditions.
- If neuronal adaption is strong, intervals are not independent
- A common measure is **correlation coefficients**:

$$c_k = \frac{\langle s_{j+k}s_j\rangle_j - \langle s_j\rangle_j^2}{\langle s^2_j\rangle - \langle s_j \rangle^2}$$

- spike-frequency adaption causes a negative correlation between subsequent intervals ($c_1 < 0$). 

- A reduced hazard immediately after a spike is a signature of neuronal refractoriness

# 5. Problem of neural coding

## 5.1 Limits of rate codes

- **Limitations of the spike count code**
  - No enough time to do temporal averaging
- **Limitations of the PSTH**
  - It needs several trials to build up
  - Needs assumption that there are populations of neurons with similar properties
- **Liminations of rate as a population average**
  - Heterogeneity of the internal parameters and connectivity pattern, which might be difficult for the postsynaptic neuron to deal with

## 5.2 Candidate temporal codes

1. rate coding with population average (mentioned above)
2. **time-to-first-spike**: only the first spike of the neuron after a signal will be counted. 
   - Brain has no time to evaluate more than one spike
3. **phase**: encode information in the phase of a pulse with respect to the background oscillation
4. **correlations and synchrony**: neurons fire collaboratively 
5. **stimulus reconstruction and reverse correlation**
   - **spike-triggered average (STA)**

    $$s^{est}(t) = \sum_{f=1}^n \kappa(t-t^{(f)})$$

   - the linear reconstruction is just the firing rate measured with a cleverly optimized time window:
    $$\nu(t) := \frac{\int K(\tau)S(t-\tau)d\tau}{\int K(\tau)d\tau} = c\sum_{f=1}^n K(t-t^{(f)})$$
    where $c = [\int K(s)ds]^{-1}$
  