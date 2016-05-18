---
layout: post
title:  "Variational free energies"
date:   2015-10-27 3:15:32
categories: [bayesian, inference]
---

Say we're really interested in some distribution $p(x;J) \propto e^{-\beta E(x;J)}$ on 
vectors $x$ and parameterized by $J$, where for the sake of discussion we have assumed an exponential model.
It is often the case that evaluating sums or integrals over $x$ is intractable, i,e. we can't evaluate things like
$\langle O\rangle = \sum_x O(x) p(x;j)$. A common way to proceed is to propose a distribution
you can work with, say $q(x;\theta)$, now paramterized by $\theta$ and then to fiddle with $\theta$ 
until $q$ looks like $p$. Formally, we want to minimize:

$$\begin{equation}
    D_{\text{KL}}(p||q) = \sum_x q(x;\theta) \log\frac{q(x;\theta)}{p(x;J)} 
\end{equation}$$

At first glance evaluating this function looks just as hard as the problem we can't solve.
If we expand $D_{\text{KL}}$ using the definition $p$: 

$$\begin{eqnarray}

    D_{\text{KL}}(p||q) &=& \sum_x q(x;\theta) \log\frac{q(x;\theta)}{e^-\beta E(x;J)} + \log Z(\beta,J) \\
    \Rightarrow \sum_x q(x;\theta) \log\frac{q(x;\theta)}{e^-\beta E(x;J)} &=& D_{\text{KL}}(p||q)+\beta F(\beta,J)

\end{eqnarray}$$

Where $Z = \sum_x p(x;J)$ and we used the fact that $\sum_x q(x;\theta)=1$ and the definition
of the free energy $F=-\beta^{-1}\log Z$. Notice that 
$D_{\text{KL}}(p||q)\geq 0$ and equal to 0 only when $p(x)=q(x)$, so that minimizing the equation
on the left will have found an upper bound (and in the case of a tight bound) an approximation
to the free energy of our original model! This motivates the definition of the variational free energy
as:

$$\begin{equation}
   \beta F(\theta) = \sum_x q(x;\theta) \log\frac{q(x;\theta)}{e^{-\beta E(x;J)}} 
\end{equation}$$

Where we then want to minimize 

$$\beta F(\theta) ={ D_{\text{KL}}(p||q)+\beta F(\beta,J)}$$ 

over $\theta$. This is also called variational bayes in the literature, and is useful beyond just exponential
distributions. Now we just have to choose a distribution $q(x)$ that is easy to evaluate, and most of the time
people choose product distributions, so that if $x\in\mathcal{R}^m$, $q(x) = \prod_i q_i(x_i)$, where
each individual $q_i(x)$ is integrable. Then, since we should be able to evaluate $e^{-\beta E}$, we have
a well-defined and tractable objective.

### Notes:

We can also write

$$\begin{equation}
    \beta F(\theta) = \beta\langle E(x;J)\rangle_{q(x)} - S[q(x)]
\end{equation}$$
 
To really make it look like an entropy. [Arxiv:1505.0542](http://arxiv.org/pdf/1505.05424v2.pdf) 
proposes a simple scheme for stochastic gradient descent on this quantity in the context of neural
networks.



