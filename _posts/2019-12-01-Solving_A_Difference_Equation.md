---
layout: post
author: Franklin Lu
title: "Solving a Difference Equation"
excerpt: A difference equation pops up in a derivation of the Poisson Process, which reminds an old dog of some calculus he learned back in physics.
math: true
date: 2019-12-01
---

This equation shows up when considering a derivation for the Poison process when considering a small timestep, $$\Delta t$$.

\\[ q_k (t + \Delta t) - q_k(t) = \lambda \Delta t [q_{k-1}(t) - q_k(t)] \\]

Which becomes:

\\[ \frac{dq_k(t)}{dt} = \lambda [q_{k-1}(t) - q_k(t)] \\]

We also have as boundary conditions, $$q_0(0) = 1$$, and $$q_k(0) = 0$$ for $k > 0$. (This comes from the construction, which I won't get into here, but makes sense because $$q$$ is a probability, namely $$q_k(t) = Pr(X_t = k)$$, and the process $$X_t$$ starts at $$0$$).

First, we have:

\\[\frac{dq_0(t)}{dt} = -\lambda q_0(t) \\]
\\[ q_0(t) = C_0e^{-\lambda t} = 1\\]
\\[ q_0(t) = e^{-\lambda t} \\]

Next, let us just solve for $$q_1$$ to get a feel for what is going on (also, taking up the dot notation to indicate time derivatives, and omitting the function argument $$t$$ for $$q_k$$'s):
\\[ \dot q_1 = \lambda[e^{-\lambda t} - q_1] \\]
\\[ \dot q_1 + \lambda q_1 = \lambda e^{-\lambda t} \\]

We find solutions to the homogenous equation:
\\[ \dot q_1 + \lambda q_1 = 0 \\]

Which are of the form:
\\[ q_1(t) = C_1e^{-\lambda t} \\]

Here, however, $$C_1$$ is not a constant but instead $$C_1(t)$$, which solves the inhomogeneous equation, so we have:

\\[ \dot C_1(t) e^{-\lambda t} -\lambda C_1(t) e^{-\lambda t} + \lambda C_1(t) e^{-\lambda t} = \lambda e^{-\lambda t} \\]
\\[ \dot C_1(t) = \lambda \\]
\\[ C_1(t) = \lambda t\\]
\\[ \dot q_1(t) = \lambda t e^{-\lambda t} \\]

In general, we have:
\\[ \dot q_k + \lambda q_k = \lambda q_{k-1} \\]
\\[q_k = C_k(t) e^{-\lambda t} \\]
\\[\dot C_k(t) e^{-\lambda t} - \lambda C_k(t) e^{-\lambda t} + \lambda C_k(t) e^{-\lambda t} = \lambda q_{k-1}\\]
\\[\dot C_k(t) e^{-\lambda t} = \lambda q_{k-1} = \lambda C_{k-1}(t) e^{-\lambda t} \\]
\\[\dot C_k(t) = \lambda C_{k-1}(t)\\]

Finally, we have from the last line:
\\[C_k(t) = \int C_{k-1}(t)dt\\]
\\[C_0 = 1\\]
\\[C_1 = \lambda t\\]
\\[C_2 = \lambda^2 \frac{t^2}{2!} \\]
\\[...\\]
\\[C_k = \frac{(\lambda t)^k}{k!}\\]
\\[q_k(t) = e^{-\lambda t} \frac{(\lambda t)^k}{k!}\\]
