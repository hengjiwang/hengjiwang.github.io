---
title: Noisy Input Models
date: 2018-12-29 01:01:04
tags:
- neurons
categories:
- neuronal dynamics
---

# 1. Noise input

$$I(t) = I^{\text{det}}(t) + I^{\text{noise}}(t)$$

Then 

$$\tau_m \frac{du}{dt} = f(u) + RI^{\text{det}}(t) + RI^{\text{noise}}(t)$$

## 1.1 White noise

Assume $R I^{\text{noise}}(t)=\xi(t)$, then for a white noise we should have

$$\langle \xi(t)\rangle = 0$$

and

$$\langle \xi(t)\xi(t')\rangle = \sigma^2 \tau_m \delta(t-t')$$

The power spectrum of white noise is the Fourier transform of $\langle \xi(t)\xi(t')\rangle$, which is flat, i.e., the noise is equally strong at all frequencies.

- **Langevin equation**:

$$\tau_m \frac{du(t)}{dt} = f(u(t)) + RI^{\text{det}}(t) + \xi(t)$$

which can be formulated as 

$$du = f(u)\frac{dt}{\tau_m} + RI^{\text{det}}(t)\frac{dt}{\tau_m} + \sigma dW_t$$

where $dW_t$ are increments of the Wiener process in a short time $dt$: $dW_t = \sigma \sqrt{dt}\mathcal{N}(0,1)$ 

White noise which is Gaussian distributed is called **Gaussian white noise**. 

- **Noisy LIF equation**:
  
$$\tau_m \frac{du(t)}{dt} = -u(t) + RI^{\text{det}}(t) + \xi(t)$$

is an **Ornstrin-Uhlenbeck process**

Analytically solve it we get

$$u(t) = {R\over\tau_{m}}\int_{0}^{t-\hat{t}}e^{-s/\tau_{m}}\,I^{(\rm det)}(t-s){\text{d}}s\,+{1\over{\tau_{m}}}\int_{0}^{t-\hat{t}}\,e^{-s/\tau_{m}}\,\xi(t-s)\,{\text{d}}s$$

The expected trajectort of the membrane potential is 

$$u_{0}(t)=\langle u(t|\hat{t})\rangle={R\over\tau_{m}}\int_{0}^{t-\hat{t}}e^{-s/\tau_{m}}\,I^{(\rm det)}(t-s)\,{\text{d}}s\,$$

For a constant input $I^{(\rm det)}(t)\equiv I_{0}$ we have 

$$u_{0}(t)=u_{\infty}\,\left[1-e^{-(t-\hat{t})/\tau_{m}}\right]\,$$

So in the absence of a threshold, the **expected trajectory** is that of the noiseless model.

The variance $\langle\Delta u^{2}\rangle=\langle[u(t|\hat{t})-u_{0}(t)]^{2}\rangle$ can be solved as 

$$\langle\Delta u^{2}(t)\rangle={1\over 2}\,{\sigma^{2}}\,\left[1-e^{-2(t-\hat{t})/\tau_{m}}\right]\,$$

which means the noise causes the membrane trajectory drift away from the expected trajectory, and also

$$\sqrt{\langle\Delta u^{2}_{\infty}\rangle}={1\over\sqrt{2}}\,{\sigma}.$$

## 1.2 Colored noise

- **colored noise**: noise of which the power spectrum is not flat
- colored noise can be generated from white noise by suitable filtering. e.g. **low-pass filtering**

$$\tau_s \frac{dI^{\text{noise}}(t)}{dt} = -I^{\text{noise}}(t) + \xi(t)$$

which is also an Ornstrin-Uhlenbeck process. Solve it we get

$$I^{\rm noise}(t)=\int_{0}^{\infty}\kappa(s)\,\xi(t-s)\,{\text{d}}s$$

where $\kappa(s)$ is an exponential low-pass filter with time constant $\tau_s$. The autocorrelation function is therefore

$$\langle I^{\rm noise}(t)I^{\rm noise}(t^{\prime})\rangle=\int_{0}^{\infty}\int_{0}^{\infty}\kappa(s)\,\kappa(s^{\prime})\,\langle\xi(t-s)\,\xi(t^{\prime}-s^{\prime})\rangle\,\,{\text{d}}s^{\prime}{\text{d}}s$$

$$ = a\,\exp(-{|t-t^{\prime}|\over\tau_{s}})$$

Therefore, knowledge of the input current at time t gives us a hint about the input current shortly afterward, as long as $|t'-t|\ll \tau_s$

The noise spectrum is the Fourier transform of $\langle I^{\rm noise}(t)I^{\rm noise}(t^{\prime})\rangle$. It's flat for $w \ll 1/\tau_s$ and falls off for $w>1/\tau_s$. $1/\tau_s$ is called **cut-off frequency**.

# 2. Stochastic spike arrival

For a neuron in a large network

$$\frac{\text{d}}{\text{d}t}u_{i},={f(u_{i})\over\tau_{m}}+{1\over C}I^{\rm
ext}(t)+\sum_{j}\sum_{t_{j}^{(f)}}w_{ij}\,\delta(t-t_{j}^{(f)})\,+\sum_{k}\sum_{t_{k}^{(f)}}w_{ik}\,\delta(t-t_{k}^{(f)})\,$$

where $w_{ij}$ is the coupling strength from a presynaptic neuron $j$ to neuron $i$; $w_{ik}$ is the weight of input from a background neuron $k$.

- **Stein's model**

Drop the neurons $j$ from the network and drop the index $i$; assume $f(u) = -u$:
  
$$\frac{\text{d}}{\text{d}t}u=-{u\over\tau_{m}}+{1\over C}I^{\rm ext}(t)+%
\sum_{k}\sum_{t_{k}^{(f)}}w_{k}\,\delta(t-t_{k}^{(f)})\,$$

Solve it we get

$$u(t|\hat{t})=u_{r}\,\exp(-{t-\hat{t}\over\tau_{m}})+{1\over C}\int_{0}^{t-\hat{t}}\exp(-{s\over\tau_{m}})\,I(t-s)\,{\text{d}}s+\sum_{k=1}^{N}\sum_{t_{k}^{(f)}}w_{k}\epsilon(t-t_{k}^{(f)})$$

where $\epsilon(s)=e^{-s/\tau_{m}}\,\Theta(s)$ is a contribution from each input spike.  

## 2.1 Membrane potential fluctuations caused by spike arrivals

Ignore the weights of the input spikes in Stein's model, then the total input spike train is 

$$S(t) = \sum_{k=1}^N\sum_{t_k^{(f)}}\delta(t-t_k^{(f)})$$

Assume the input statistics as Poisson, then 

$$\langle S(t) \rangle = \nu_0$$

and autocorrelation

$$\langle S(t)S(t')\rangle = \nu_0^2 + \nu_0\delta(t-t')$$

- The solution of Stein's model can be rewritten as

$$u(t)={1\over C}\int_{0}^{\infty}\exp(-{s\over\tau_{m}})\,I(t-s)\,{\text{d}}s+w%
_{0}\int_{0}^{\infty}\epsilon(s)\,S(t-s)\,{\text{d}}s\,$$

- The mean potential is 

$$u_{0}(t)={1\over C}\int_{0}^{\infty}\exp(-{s\over\tau_{m}})\,I(t-s)\,{\text{d}}s+w_{0}\,\nu_{0}\,\int_{0}^{\infty}\epsilon(s)\,{\text{d}}s$$

- The variance is 

$$\langle \Delta u^2\rangle \displaystyle=w_{0}^{2}\,\nu_{0}\int_{0}^{\infty}\epsilon^{2}(s)\,{\text{d}}s\,$$

## 2.2 Subthreshold vs. superthreshold regime

- **subthreshold(superthreshold) stimuli**: stimuli that generates a membrane potential below(above) the firing threshold in the absence of noise
- In the superthreshold regime, diffusive noise has little influence except for braodening the interspike interval distribution.
- For the subthreshold regime, noise can turn a quiescent neuron into a spiking one. 

## 2.3 Interval distribution in the superthreshold regime

If noise has a small amplitude $0<\sigma\ll u_{\infty}-\vartheta$, then the interval distribution has a mean $s_0$, variance can be estimated from $\langle \Delta u^2_\infty\rangle = \frac{1}{\sqrt{2}}\sigma$.

The scaling factor between the distribution of $u(t)$ and interval is $u_0'(t)$ evaluated at $t=s_0$. Since the distribution of $u(t)$ is a Gaussian distribution, the interval distribution is

$$P_{0}(t|0)={1\over\sqrt{\pi}}{u_{0}^{\prime}\over\sigma}\exp\left[-{(u_{0}^{\prime})^{2}\,(t-s_{0})^{2}\over\sigma^{2}}\right]\,$$

# 3. Fokker-Plank equation

- For $t > \hat{t}$, the **probability density of the membrane potential** is denoted as $p(u,t)$, which satisfy **Fokker-Plank equation**

$$\displaystyle\tau_{m}{\partial\over\partial t}p(u,t) = \displaystyle-{\partial\over\partial u}\left[-u+\tau_{m}\sum_{k}\nu_{k}(t)\,w_{k}\right]\,p(u,t) + {1\over 2}\,\left[\tau_{m}\sum_{k}\nu_{k}(t)\,w_{k}^{2}\right]\,{\partial^{2}\over\partial u^{2}}p(u,t)$$
