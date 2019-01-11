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
We'll need to briefly introduce a few concepts from quantum mechanics. First is the wavefunction of a particle $\psi:\Omega\rightarrow \mathbb{C}^n$, where $\Omega$ is typically $\mathbb{R}^3\times[0,\infty)$ (three-dimensional space + time) and $n=1$. The square of the modulus of the wave function gives the probability density of the particle. For $\Omega = \mathbb{R}^3\times[0,\infty)$, this means that \\[\int_{\mathbb{R}^3}|\psi(x,t)|^2 dx = 1,\; \forall t\qquad \textrm{(the normalization condition)} \\]
Thus in this typical case, the wavefunction is a square integrable function. More generally, the wavefunction of a particle is an element of a complex Hilbert space $\mathcal{H}$. The normalization condition then generalizes to $||\psi||^2=\langle\psi,\psi\rangle = 1$, where $\langle\cdot,\cdot\rangle:\mathcal{H}\times\mathcal{H}\rightarrow\mathbb{C}$ is the inner product for the Hilbert space.

The particle's physical properties (eg. position and momentum) are represented by linear operators $\mathbf{A}:\mathcal{H}\rightarrow\mathcal{H}$ such that $\langle{\mathbf{A}\psi,\phi\rangle}=\langle \psi,\mathbf{A}\phi\rangle$ for all $\psi,\phi \in \mathcal{H}$  ($\mathbf{A}$ is a *Hermitian operators*). Hermitian operators generalize the Hermitian matrices one might have encountered studying linear algebra. As with their finite dimensional counterparts, the number $\langle \mathbf{A}\rangle =\langle \psi,\mathbf{A}\psi\rangle$ is always real. What's more as a consequence of the wavefunction encoding a probability density of the particle, the number $\langle\mathbf{A}\rangle$ is actually the expectation value of the operator. In other words, if we measured multiple times the property represented by $\mathbf{A}$ on a particle with wavefunction $\psi$, the average of these measurements will be $\langle\mathbf{A}\rangle$.$^1$

Finally, the uncertainty in a measurement of a physical property is given by standard deviation of the operator \\[\sigma_\mathbf{A}^2 = {\langle\mathbf{A}^2\rangle - \langle\mathbf{A}\rangle^2}\\] 

#### Proof of the Uncertainty Principle










---
###### $^1$ You might have observed that the symbol $\langle\mathbf{A}\rangle$ does not make reference to the wavefunction used to calculate. This is partly because this wavefunction is normally made obvious beforehand and partly because the measurement of an observable induces a "wavefunction collapse", where the wavefunction after measurement is an eigenvector of $\mathbf{A}$.  








 
