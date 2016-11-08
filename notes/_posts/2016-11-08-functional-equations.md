---
layout: post
title: "Functional equations"
date: 2016-11-08 2:03:00
categories: [statistical-mechanics]
---

Functional equations show up a lot in results of the renormalization group. For example, $f(x^3)=f(x)/3$ represents the the analytic flow equation of the 1D Ising model under decimation. Another example is the scaling function of correlations of scaling fields:

\\[ G(r/b) = b^{2x}G(r) \\]

I have found the solutions of these functional equations mysterious, so I present their solutions below. The general scheme is that of perturbation theory.

### Solving $ G(r/b) = b^{2x}G(r) $
Assume $b=1+\epsilon$ where $\epsilon \ll 1$, so that this is a perturbative rescaling of $r$.  In this case we can expand the small parameter $\epsilon$:

$$ G\left(\frac{r}{1+\epsilon}\right) \sim G(r(1-\epsilon)) \sim G(r) - \epsilon r G^\prime(r) $$

is the left-hand side of the functional equation. The right-hand side is

$$ (1+\epsilon)^{2x} G(r) \sim (1 + 2x\epsilon) G(r) $$

To first order in $\epsilon$ our functional equation reads

$$ G(r) - \epsilon r G^\prime(r) = (1+2x\epsilon)G(r) $$

$G(r)$ cancels on both sides, and then $\epsilon$ cancels! The result is a seperable differential equation

$$ \frac{G^\prime(r)}{G(r)} = -\frac{2x}{r} $$

which has the solution

$$ G(r) = \frac{C}{r^{2x}} $$

For some constant $C$. This is the classic 'scaling dimension' result.

### Solving $ n f(x^n) = f(x) $
In the context of block-spin Renormalization this equation clearly intends for $n\in\mathbb{Z}$, but we can assume $n$ is any nonzero number.  This equation clearly has no unique solution for $n=1$. So to proceed with our perturbation analysis let's assume $n=1+\epsilon$.  In this case the trickiest part is expanding $x^{1+\epsilon}$. This can be done by writing it as

$$ e^{(1+\epsilon)\log{x}} \sim x(1+\log{x}) $$

Expanding the functional equation and simplifying as above yields another seperable differential equation

$$ f(x) = - x\log{x} f^\prime(x) $$

which has the solution

$$ f(x) = \frac{C}{\log{x}} $$

For some positive constant $C$. This is the result that allows the RG of the 1D Ising model to predict exponentially decreasing correlations at all finite temperatures.


