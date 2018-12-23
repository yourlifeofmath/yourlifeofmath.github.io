---
layout: post
author: Franklin Lu
title: Rope Between Two Inclines
excerpt: A rope rests on two platforms which are both inclined at an angle. The rope has uniform mass density, and its coefficient of friction with the platforms is 1. What is the largest possible fraction of the rope that does not touch the platforms?
date: 2018-10-27
math: true
---
### Q:
A rope rests on two platforms which are both inclined at an angle $\theta$ (which you are free to pick). The rope has uniform mass density, and its coefficient of friction with the platforms is $1$. The system has left-right symmetry. What is the largest possible fraction of the rope that does not touch the platforms? What angle $\theta$ allows this maximum value?

### A:
Split the rope into three parts: the first is of mass $x$ on the left incline, the second is of mass $x$ on the right incline, and the third is of mass $m - 2x$, which is between the inclines. Consider first the forces on the first part of the rope (which is the same as for the second part, due to the symmetry of the problem). There is the component of the force of gravity pulling the rope into the incline, equal and opposite to the normal force. Thus:

\\[ F_n = F_g \cos\theta = gx \sin\theta \\]

There is also the force of friction which is opposite the force pulling the rope down the incline, which is equal to the sum of the component of the force of gravity down the incline and the tension of the third part of the rope on the first, and thus:

\\[ F_f = \mu F_N = gx \sin\theta \\]
\\[ F_f = F_g \sin\theta + F_T \\]

Then, we can solve for $F_T$, to be used later:
\\[ F_T = gx \sin\theta - gx \cos\theta \\]

The forces are balanced for the hanging part of the rope as well. Due to symmetry, the $x$-components will always balance, and we see that for the net force to be zero in the $y$-component, we require:

\\[ 2F_T \sin\theta = F_G \\]
\\[ gx \sin\theta - gx \cos\theta = (m - 2x)g \\]

We can then solve to obtain:

\\[ x = \frac{m}{2 + \cos\theta \sin\theta - \sin^2\theta} \\]

Then, if we take derivatives with respect to $\theta$, and set equal to zero, we obtain:

\\[ 0 = -m\frac{\cos^2\theta - \sin^2\theta - 2\sin\theta \cos\theta}{(2 + \cos\theta \sin\theta - \sin^2\theta)^2} \\]

\\[ 0 = \cos^2\theta - \sin^2\theta - 2\sin\theta \cos\theta = \cos2\theta - \sin2\theta \\]

\\[ \tan2\theta = 1 \\]

\\[ \theta = \frac{\pi}{8} \\]

Then, the maximum value of $x$ is achieved by plugging in $\theta = \frac{\pi}{8}$.