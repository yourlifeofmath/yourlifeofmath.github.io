---
layout: post
author: Franklin Lu
title: N Lines on a Circle
excerpt: Given N lines distributed randomly along the outside of a circle, we can ask some interesting questions.
date: 2018-10-02
math: true
---
Given $N$ lines distributed randomly along the outside of a circle, we can ask some interesting questions.

#### For starters, what is the chance that, for $N = 2$, we have an intersection?
We can solve this by picking four arbitrary points to be endpoints of the lines, and index them $1, 2, 3, 4$. If we randomly connect them (we can specify the connections by specifying which endpoint 1 pairs with, as the remaining two will pair), we see that $1$ and $3$ yields an intersection, while $1$ and $2$, $1$ and $4$ do not. Thus, the chance of two lines intersecting is $\frac{1}{3}$.

#### What is the expected number of intersections for N lines?
We initially thought this might be a hard problem when we posed it, because we thought of it as we were considering the distribution of intersections for $N$ lines. That turns out to be a much harder question, because linearity of expectation saves the day and makes computing expectation easy. First, index the lines $1, \dots, n$. Let $X_{ij}$ denote the event that line $i$ intersects line $j$, and let $X_i$ denote the sum of $X_{ij}$ over all $j$, which is the total number of times line $i$ is intersected. Then, let $X$ be the sum of all $X_i$ over all $i$. We want to find $E[X]$.

We notice that $X_{ij}$ is just the question we answered already: the chance two random lines intersect is $\frac{1}{3}$. But then, by linearity of expectation, we have $E[X_i] = \frac{1}{3}(n-1)$, and $E[X] = \frac{1}{3}(n)(n-1)$. But at this point, we have both counted $i$ intersecting $j$ and $j$ intersecting $i$, and so we need to divide by $2$ to eliminate the effect of double counting, and we get that the expected value is $\frac{n(n-1)}{6}$.

#### What is the distribution for the number of intersections?
This is a harder question. Let us start with no intersections: given $N$ lines, what is the probability of getting no intersections?

First, we notice that any way of drawing $N$ lines means we start with $2N$ points, and connect them $2$ at a time. Let $F_{N}$ denote the number of ways of connecting $N$ lines without intersections. Let us label the points $1, 2, \dots, 2N$ clockwise, with the point $1$ at the very bottom of the circle. If we connect $1$ and $2$, there is a block of $2N-2$ points to the right, which we can connect without intersections in $F_{N-1}$ ways. If we connect $1$ and $3$, we notice that $2$ must connect with one of the points to the right. If we connect $1$ and $4$, we see that to have no intersections, $2$ and $3$ must connect (this can be thought of as $F_{1}$, or one possible line), and the block of $2N-4$ points to the right must connect without intersections (and there are $F_{N-2}$ such ways to do this). In general, we see that if we draw an arbitrary first line consisting of 1 and point $i$, we can prevent intersections so long as: 

1. we do not intersect that first line, which means no point in the left block connects to a point in the right block,

2. we do not have an odd number of points in each block, which forces one point to connect with another point,

3. we do not intersect within blocks.

Thus, given a first line, the number of ways to create no intersections is to multiply the number of ways to do so given the $i - 2$ points in the first block times the number of ways to do so given the $2N - i$ points in the second block. We also notice that when dealing with $2N$ points, it is as though we deal with $N$ lines. This gives us a nice recursive relationship by summing up over all initial lines:

\\[ F_N = F_{N-1}F_{0} + F_{N-2}F_{1} + ... + F_{1}F_{N-2} + F_{0}F_{N-1} \\]

But, we know that this is precisely the formula for the $N$th Catalan number! Thus,

\\[ F_N = C_N = \frac{1}{N+1}{2N \choose N} = \frac{(2N)!}{(N+1)!N!} \\]

Then, we simply want to divide by the total number of ways to arrange $N$ lines, without care for intersections. To place a first line, we start with any starting point, and note that there are $2N-1$ options for an endpoint. The second line corresponds to $2N-3$ options, and so on. Thus, our total number of ways to arrange $N$ lines on a circle, $T_N$, will be:

\\[ T_N = (2N - 1)(2N-3)...(3)(1) = \frac{(2N)!}{(2N)(2N-2)...(4)(2)} = \frac{(2N)!}{2^N N!} \\]

And so, the probability of having zero intersections in N lines is:

\\[ \frac{F_N}{T_N} = \frac{(2N)!}{(N+1)!N!}\frac{2^NN!}{(2N)!} = \frac{2^N}{(N+1)!} \\]