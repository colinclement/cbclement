---
layout: post
title:  "Gradients of Negative log-Likelihood"
date:   2015-10-14 12:57:14
categories: current reconstruction
---

## Notation
The measured flux image is denoted $\phi^0$. A model of the flux of an external current loop is denoted $\phi_{ext}$.
The current dipole field is denoted $g$, the external loop dipole field is $g_{ext}$, and the matrix which encodes 
the Biot-Savart law and the point-spread is denoted $M$, so that $\phi = M g$. 
The cost or negative log-likelihood of observing a flux $\phi$ due to a dipole field $g$ is written:

$$
\mathcal{L} = \frac{1}{2\sigma^2}|| {(\phi^0 - \phi_{ext}) - Mg||^2 + \frac{\mu}{2} || \Gamma (g + g_{ext})|}|^2
$$

Where $\Gamma$ is a regularization operator formed as an orthogonal projection. 
$\Gamma = I-W W^T$ where $W$ has columns containing features we would like to be in
the solution $g$. In other words, there is a prior on $g$ that penalizes the sum of squared features
that are not in the span of $W$. In other other words, we hide the features of $g$ 
we'd like to see in the null space of $\Gamma$.

## Gradients of $\mathcal{L}$

### Gradient w.r.t. $z$

Denote all parameters of $M$ by $z$, so that $M=M(z)$. These include the height of the measurement
plane above the current plane, and the PSF parameters. So far the only other parameter considered
is the total current of the external loop, $J_{ext}$. This is defined so that 
$\phi_{ext} =  J_{ext} M g_{ext} $, where the external loop was modeled with net unit current.
Then the gradients of $\mathcal{L}$ with respect to the $z$ parameters is:

$$
\begin{equation}
\frac{\partial \mathcal{L}}{\partial z} = \frac{-1}{\sigma^2} r^T \left(\frac{\partial \phi_{ext}}{\partial z} + 
                                                  \frac{\partial M}{\partial z} g\right)
\end{equation}
$$

Where $r =  {(\phi^0 - \phi_{ext}) - Mg}$ is the residual. Note that 
$\frac{\partial \phi_{ext}}{\partial z} = \frac{\partial M}{\partial z} g_{ext}$, except with a 
kernel $M$ which is much larger than that of the reconstructed image. That's why we can't simplify
the above gradient.

### Gradient w.r.t. $J_{ext}$

If we write $\phi_{ext} = J_{ext} \phi_{ext}^0$ and $g_{ext} = J_{ext} g_{ext}^0$, we can take a
derivative of $\mathcal{L}$ with respect to the total external current loop. $g_{ext}^0$ is the
current dipole field for a unit total current, so that $J_{ext}$ is the total external current.
The result is:

$$
\frac{\partial \mathcal{L}}{\partial J_{ext}} = \frac{-1}{J_{ext}\sigma^2}({r^T \phi_{ext} + 
                                                                  \mu (g + g_{ext})^T \Gamma g_{ext}})
$$

It's useful to consider the fact that for us $\Gamma^T = \Gamma$ and $\Gamma^2 g = \Gamma g$.

We can set $\frac{\partial \mathcal{L}}{\partial J_{ext}}=0$ to find the optimal $J_{ext}$, the result of
which is 

$$
{J_{ext}} = \frac{(\phi^0 - Mg)^T \phi_{ext}^0 + \mu g^T \Gamma g_{ext}^0}
{-\phi^{0T}_{ext} \phi^{0}_{ext}+ \mu g_{ext}^{0T} \Gamma g_{ext}^{0}}
$$

Since $\mu$ is quite small, on the order of $1/\text{SNR}$, and also because the inner products
that $\mu$ prepends are small, it will be useful to consider the $\mu \rightarrow 0$ limit:

$$
{J_{ext}} \approx \frac{(\phi^0 - Mg)^T \phi_{ext}^0 } {-\phi^{0T}_{ext} \phi^{0}_{ext}}
$$

So the optimal $J_{ext}$ is approximately the projection of the residual onto the external loop field.
That is, if the residual doesn't look much like the external loop field, then the optimal current
will be very low. That makes sense.


### Standard least-square form

The above least-squares problem is easier to fit into a software package if we write it in the
following form:

$$
\begin{equation}

\frac{1}{2}\left|\left|  \begin{bmatrix} \frac{1}{\sigma}(\phi^0 - \phi_{ext}) \\ 
                                         -\sqrt{\mu} \Gamma g_{ext} \end{bmatrix} - 
                 \begin{bmatrix} \frac{1}{\sigma}M \\ \sqrt{\mu}\Gamma \end{bmatrix} g\right|\right|^2

    = \frac{1}{2}|| \Phi - Ag ||^2 = \frac{1}{2}R^TR
\end{equation}
$$

Where $R = \Phi - Ag $. Then gradients are in a somewhat simpler form: 
$$
\begin{equation}
\frac{\partial \mathcal{L}}{\partial z} = R^T\frac{\partial R}{\partial z}
\end{equation}
$$




