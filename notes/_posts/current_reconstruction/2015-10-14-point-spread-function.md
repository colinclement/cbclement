---
layout: post
title:  "Point spread functions"
date:   2015-10-14 5:31:20
categories: current reconstruction
---

## Properties & Notation

Measured flux $\phi(x,y) = \int B_z(x-x_0,y-y_0)\rho(x_0, y_0) dx_0 dy_0$ where $B_z$ is the magnetic field
perpendicular to the plane of current.

### Basic Gaussian

To start I used a simple 2-parameter Gaussian, parametrized in $k$-space.
$\rho(k_x, k_y) = e^{-2\pi^2 ((\sigma_x k_x)^2+(\sigma_y k_y)^2)}$. In real space this is just
$\rho(x, y) = \frac{1}{2 \pi \sigma_x \sigma_y} e^{-\frac{1}{2}((x/\sigma_x)^2+(y/\sigma_y)^2)}$

The gradients with respect to the variances are then

$$
\frac{\partial \rho(x,y)}{\partial \sigma_x} = \rho(x,y)\left( \frac{x^2}{\sigma_x^3}-\frac{1}{\sigma_x}\right) 
$$
(Similarly for $\sigma_y$).

### Two Gaussians

Sum of two Gaussians to try to get the smear of the SQUID loop key-shape
