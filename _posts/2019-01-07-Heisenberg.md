---
layout: post
author: Frimpong Baidoo
title: Heisenberg's Uncertainty Principle
excerpt: We'll prove the uncertainty principle using the Cauchy-Schwarz inequality. 
math: true
---

### Q:
Show that the uncertainty in measurement of a particle's position $$\sigma_x$$ and the uncertainty in its momentum  $$\sigma_p$$ are such that \\[\sigma_x\sigma_p \ge \frac{\hbar}{2}\\]  where $\hbar$ is the reduced Planck's constant.

### A:
We'll first need to be acquainted with a few concepts from quantum mechanics. First is the wavefunction of a particle $\psi:\Omega\rightarrow \mathbb{C}^n$, where $\Omega$ is typically $\mathbb{R}^3\times[0,\infty)$ (Euclidean space + time) and $n=1$. The square of the modulus of the wave function gives the probability density of the particle. For $\Omega = \mathbb{R}^3\times[0,\infty)$, this means that \\[\int_{\mathbb{R}^3}|\psi(x,t)|^2 dx = 1,\; \forall t\qquad \textrm{(the normalization condition)} \\]
Thus the wavefunction has to be a square integrable function. More generally, the wavefunction of a particle is an element of a Hilbert space $\mathcal{H}$. Thus the normalization condition is given by $\langle\psi,\psi\rangle = 1$, where $\langle\cdot,\cdot\rangle:\mathcal{H}\times\mathcal{H}\rightarrow\mathbb{C}$ is the inner product for the Hilbert space.















































 
