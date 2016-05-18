---
layout: post
title: "Bayesian approach to current reconstruction"
date: 2015-10-12 5:56:00
categories: current reconstruction
---


This is based on Ali Mohammad-Djafari's 'A Full Bayesian Approach for Inverse Problems.'

Our data is called $\phi^0\in\mathcal{R}^m$, and we have a parameterized relationship between $\phi^0$ 
and unknown parameters $g\in\mathcal{R}^n$, the local dipole current field. We assume $\phi^0 = M(z) g + \eta$ 
where $\eta$ is some Gaussian white noise of size $1/\sigma^2$ and $M\in\mathcal{R}^{m\times n}$ 
includes both the Biot-Savart law and the point spread function of the SQUID loop (parameterized by $z$). 
we can control the dimension $n$ of $g$, and if we make $n<m$ we can increase the noise-tolerance of the
problem. Usually $n = m/a^2$ where $a$ is 2 or 3 for example.

Our hypothesis can be expressed probabilistically as:
$$\begin{equation}
P(\phi | g, z, \sigma) = \frac{1}{(2\pi\sigma^2)^{m/2}}\exp\left(\frac{-1}{2\sigma^2}||\phi^0-Mg||^2 \right)
\end{equation}$$

This problem is in general referred to as blind deconvolution. Because it is ill-posed, we have have to include
prior information to obtain a solution that is not totally corrupted by the experimental noise. A Gaussian
prior on $g$ can be expressed as
$$\begin{equation}
P(g|\mu) = \left(\frac{\mu^2}{2\pi}\right)^{n/2}\exp\left( -\frac{\mu}{2}||\Gamma g||^2\right)
\end{equation}$$

# Cramer-Rao bound

The minimum variance of a parameter $\xi$ of a measured image $I$ is:

$$
{\sigma_\xi^2} = \frac{1}{\text{SNR}^2} \left( \sum_i \left(\frac{\partial I_i}{\partial \xi}\right)^2\right) 
$$

Where $i$ indexes pixel measurements. For us this is $I_i = \phi_i = M_{ik}g_k$. (Derivation to come).


