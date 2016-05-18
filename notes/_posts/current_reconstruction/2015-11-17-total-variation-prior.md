---
layout: post
title:  "Total Variation Prior"
date:   2015-11-17 2:17:33
categories: current-reconstruction
---
 
[In another post]({% post_url notes/_posts/current_reconstruction/2015-10-14-gradients-of-nll %}) 
I computed the negative-loglikelihood of an image given current dipole fields $g$ with
a quadratic prior probability on $g$. The quadratic priors penalize sharp edges too much,
causing the reconstruction to suffer near line currents. To remedy this I switch to a 
total variation (TV) regularization, which imposes sparse gradients on the image:

$$
\begin{eqnarray}
    p(g) &=& C\exp\left(-\lambda TV(g)\right) \\ 
    \text{where  } TV(g) &=& \int | \nabla g |^2 d^2x
\end{eqnarray}
$$

This prior favors images with constant patches, where only the boundaries contribute to
$TV(g)$ and reduce the probability. Since we're mostly interested in the currents, which are
the derivatives of $g$, we will instead impose a sparsity of the second derivatives or
equivalently a sparsity of the second derivatives of $g$:

$$\begin{eqnarray}
    p(g) &=& C\exp(-\lambda TV_2(g)) \\
    \text{where  } TV_2 &=& \sum_i \sqrt{(D_h^2g_i)^2+(D_v^2g_i)^2 }
\end{eqnarray}$$

for horizontal ($x$) derivatives $D_h$ and vertical ($y$) derivatives $D_v$. Then, as in 
[Gradients of NLL]({% post_url currentreconstruction/2015-10-14-gradients-of-nll %}) we define

$$
\mathcal{L} = \frac{1}{2\sigma^2}\left(|| {(\phi^0 - \phi_{ext}) - Mg}||^2 + 
2\sigma^2\mu TV_2(g+g_{ext})\right)
$$


