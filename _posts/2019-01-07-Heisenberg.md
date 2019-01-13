---
layout: post
author: Frimpong Baidoo
title: Heisenberg's Uncertainty Principle
excerpt: We'll prove the uncertainty principle using basic principles from probability and statistics. 
math: true
---

### Q:
Show that the uncertainty in measurement of a particle's position $$\sigma_\mathbf{x}$$ and the uncertainty in its momentum  $$\sigma_\mathbf{p}$$ are such that \\[\sigma_\mathbf{x}\sigma_\mathbf{p} \ge \frac{\hbar}{2}\\]  where $\hbar$ is the reduced Planck's constant.

### A:
We'll need to briefly introduce a few concepts from quantum mechanics. First is the wavefunction of a particle $\psi:\Omega\rightarrow \mathbb{C}^n$, where $\Omega$ is typically $\mathbb{R}^3\times[0,\infty)$ (three-dimensional space + time) and $n=1$. The square of the modulus of the wave function gives the probability density of the particle. For $\Omega = \mathbb{R}^3\times[0,\infty)$, this means that \\[\int_{\mathbb{R}^3}|\psi(x,t)|^2 dx = 1,\; \forall t\qquad \textrm{(the normalization condition)} \\]
Thus in this typical case, the wavefunction is a square integrable function. More generally, the wavefunction is an element of a complex Hilbert space $\mathcal{H}$. The normalization condition generalizes to $||\psi||^2=\langle\psi,\psi\rangle = 1$, where $\langle\cdot,\cdot\rangle:\mathcal{H}\times\mathcal{H}\rightarrow\mathbb{C}$ is the inner product for the Hilbert space.

The particle's physical properties (or observables) are represented by linear operators $\mathbf{A}:\mathcal{H}\rightarrow\mathcal{H}$ such that $\langle{\mathbf{A}\psi,\phi\rangle}=\langle \psi,\mathbf{A}\phi\rangle$ for all $\psi,\phi \in \mathcal{H}$  (i.e. $\mathbf{A}$ is a *Hermitian operator*). Hermitian operators generalize the Hermitian matrices one might have encountered studying linear algebra. Thus just like their finite dimensional counterparts, they guarantee that the number $\langle \mathbf{A}\rangle =\langle \psi,\mathbf{A}\psi\rangle$ is always real. What's more as a consequence of the wavefunction encoding the probability density of the particle, the number $\langle\mathbf{A}\rangle$ is actually the expectation value of the operator. That is, we can think of the operator as a random variable in which case $\langle\mathbf{A}\rangle$ is just a fancy way of writing $\textrm{E}[\mathbf{A}]$.

The uncertainty in a measurement of a physical property is given by standard deviation of the operator \\[\sigma_\mathbf{A}^2 = \langle\left(\mathbf{A}-\langle\mathbf{A}\rangle\right)^2\rangle= {\langle\mathbf{A}^2\rangle - \langle\mathbf{A}\rangle^2} \\]

#### Proof of the Uncertainty Principle

Given any two observables $\mathbf{A}$ and $\mathbf{B}$, we will prove that \\[\sigma_\mathbf{A}^2\sigma_\mathbf{B}^2\ge\left(\frac{\langle[\mathbf{A},\mathbf{B}]\rangle}{2\mathit{i}}\right)^2 \qquad\qquad\qquad(\mathbf{1})\\] where $[\mathbf{A},\mathbf{B}] = \mathbf{A}\mathbf{B}-\mathbf{B}\mathbf{A}$ is an antihermitian operator called the commutator of $\mathbf{A}$ and $\mathbf{B}$. 

To do this we assume a known wavefunction $\psi$ and introduce the variables 
$\mathit{a} = (\mathbf{A}-\langle\mathbf{A}\rangle)\psi\;$ and $\; \mathit{b} = (\mathbf{B}-\langle\mathbf{B}\rangle)\psi$.

Because the operators are Hermitian, we find that $\;\sigma_\mathbf{A}^2=\langle(\mathbf{A} -\langle\mathbf{A}\rangle)^2\rangle=\langle\mathit{a},\mathit{a}\rangle\;$ and $\;\sigma_\mathbf{B}^2=\langle\mathit{b},\mathit{b}\rangle$. What's more, we also have that $\;\langle\mathit{a},\mathit{b}\rangle = \langle(\mathbf{A}-\langle\mathbf{A}\rangle)(\mathbf{B}-\langle\mathbf{B}\rangle)\rangle =\langle\mathbf{A}\mathbf{B}\rangle-\langle\mathbf{A}\rangle\langle\mathbf{B}\rangle,\;$ where the last equality is due to the linearity of expectation. 

Thus the Cauchy-Schwarz inequality applied to $\mathit{a}$ and $\mathit{b}$ gives \\[\sigma_\mathbf{A}^2\sigma_\mathbf{B}^2\;\ge\;\langle\mathbf{A}\mathbf{B}\rangle-\langle\mathbf{A}\rangle\langle\mathbf{B}\rangle\\]
Finally, we note that $\|\langle\mathit{a},\mathit{b}\rangle\|^2\ge \textrm{Im}(\langle\mathit{a},\mathit{b}\rangle)^2 = \left(\frac{\langle\mathbf{A}\mathbf{B}\rangle-\langle\mathbf{B}\mathbf{A}\rangle}{2\mathit{i}}\right)^2$ and use the linearity of expectation to obtain the right hand side of the inequality $(\mathbf{1})$.

The momentum operator is such that $\,\mathbf{p}\psi = \frac{\hbar}{\mathit{i}}\nabla\psi\;$ whilst the position operator is such that $\,\mathbf{x}\psi=x\psi$. Both are Hermitian operators on the space of square integrable functions. Thus the expected value of the commutator is going to equal $\mathit{i}\hbar$, which when plugged into the righthand side of $(\mathbf{1})$ yields the classic Heisenberg uncertainty principle. 















 
