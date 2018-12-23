---
layout: post
author: Franklin Lu
title: Falling Off a Hemisphere
excerpt: A point particle of mass m sits at rest on top of a frictionless hemisphere of mass M, which rests on a frictionless table. The particle is given a tiny kick and slides down the hemisphere. At what angle (measured from the top of the hemisphere) does the particle lose contact with the hemisphere?
date: 2018-10-24
math: true
---
### Q:
A point particle of mass m sits at rest on top of a frictionless hemisphere of mass $M$, which rests on a frictionless table. The particle is given a tiny kick and slides down the hemisphere. At what angle $\theta$ (measured from the top of the hemisphere) does the particle lose contact with the hemisphere? In answering this question for $m \neq M$, it is sufficient for you to produce an equation that $\theta$ must satisfy (it will be a cubic). However, for the special case of $m = M$, this equation can be solved without too much difficulty; find the angle in this case.

### A: Case Where M is Infinite
This problem actually came up in my first year physics class (and maybe even high school, come to think of it). It is an instructional problem in the sense that it teaches students how sometimes considering an energy argument can bypass a lot of trouble that would arise in considering solving for motion explicitly.

The essential argument is that, at any point, the total energy in the system is equal to $E = mgR$, which is to say that the total energy is always equal to the initial gravitational potential energy. If we consider some later time, when the particle is at an angle $\theta$, we see that its energy is $U = mgRcos\theta$ in potential energy plus its kinetic energy, $\frac{1}{2}mv^2$. If we consider the net force in the plane perpendicular to motion, we see that it involves the gravitational force perpendicular to motion, $F_G = mgcos\theta$ and the normal force of the hemisphere on the particle, $F_N$, and we know that this net force should be a centripetal force. Thus, we have $F_{\perp} = F_G + F_N = \frac{mv^2}{R}$, and we know that the particle loses contact when $F_N$ is zero, and so we have this condition on $\theta$ for when the particle loses contact:

\\[ mg \cos\theta = \frac{mv^2}{R} \\]

Then, we use the fact that energy is conserved:

\\[ mgR = mgRcos\theta + \frac{1}{2}mv^2 \rightarrow 2mg(1 - cos\theta) = \frac{mv^2}{R} \\]

Which we then can combine with our condition on $\theta$ to get:

\\[ mg \cos\theta = 2mg(1 - \cos\theta) \rightarrow \cos\theta = \frac{2}{3} \\]

### A: General Case
In the general case, we have more moving parts to consider, but the basic argument will be the same. We will consider the total energy of the system, which should still be constant and equal to the initial potential energy, and then impose as condition on $\theta$ based on the fact that we expect the net force to be equal to a centripetal force at all times, with the gravitational force being the only contribution when the particle leaves the hemisphere.

When things start moving, we will notice that there will be two separate motions: the hemisphere moving to the left, and the particle moving to the right in the direction tangent to the hemisphere. We can break down the motion of the particle into x- and y-components, and write the conservation of energy as follows (with $(x, y)$ as the position of the particle from the origin (the center of the hemisphere, initially), $X$ being the x-position of the hemisphere from the origin, $R$ as the radius of the hemisphere, $m$ as the mass of the particle, and $M$ as the mass of the hemisphere).

\\[ mgR = mgR \cos\theta = \frac{1}{2}m\dot{x}^2 + \frac{1}{2}m\dot{y}^2 + \frac{1}{2}M\dot{X}^2 \\]

However, we also want to write everything in terms of $\dot{x}$. Using a center of mass argument, we reason that as no net force acts on the system in the horizontal direction, the center of mass must remain at the origin, and so we have:

\\[ MX + mx = 0 \rightarrow \dot{X} = -\frac{m}{M}\dot{x} \\]

For the rest of the problem, we want to work in the frame where the hemisphere is at rest (or, a frame moving to the right with velocity $\dot{X}$. This will allow us to consider the net velocity of the particle. We notice that the net velocity of the particle relative to the hemisphere, at an angle $\theta$, is given by:

\\[ v_x = \dot{x} - \dot{X} = v_{net} \cos\theta \rightarrow v_y = \dot{y} = v_{net} = v_{net} \sin\theta \\]

\\[ \dot{y} = (\dot{x} - \dot{X}) \tan\theta = \dot{x}(1 + \frac{m}{M}) \tan\theta \\]

Thus, we may rewrite our conservation of energy in terms of $\dot{x}$ (equation (1)):

\\[ 2gR(1- \cos\theta) = \dot{x}^2[1 + (1 + \frac{m}{M})^2 \tan^2\theta + \frac{m}{M}] \\]

Now, in this frame, only the particle is moving, and the only force it experiences is gravity. Thus, by the same argument, if it experiences a centripetal force, and the normal force is zero, then the force of gravity must be equal to the centripetal force, and we have:

\\[ mg \cos\theta = \frac{mv_{net}^2}{R} = \frac{m\dot{x}^2(1 + \frac{m}{M})^2}{R \cos^2\theta} \\]

Or, solving for $\dot{x}^2$ (equation (2)):

\\[ \dot{x}^2 = \frac{Rg \cos^3\theta}{(1 + \frac{m}{M})^2} \\]

Then, with combining equations (1) and (2), we get:

\\[ 1 = cos\theta + \frac{1}{2}[ \frac{\cos^3\theta}{(1 + \frac{m}{M})^2} ][1 + (1 + \frac{m}{M})^2 \tan^2\theta + \frac{m}{M}] \\]

If we do a quick sanity check, and we take $\frac{m}{M} = 0$, which corresponds to the case where our hemisphere does not move, we recover the previous equation (with some algebra):

\\[ \cos\theta = \frac{2}{3} \\]

If we use $\frac{m}{M} = 1$, then we get the equation (with some algebra):

\\[ \cos^3\theta - 6 \cos\theta + 4 = 0 \\]

This equation can be solved to give:

\\[ \cos\theta = 2, -1 - \sqrt{3}, \sqrt{3} - 1 \\]

Only the last solution is physical ($\theta$ ranges from 0 to $\frac{\pi}{2}$, so $\cos\theta$ ranges from $0$ to $1$).