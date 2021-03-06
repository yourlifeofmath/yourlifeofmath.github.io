---
layout: post
author: John Zhao
title: Connecting Red and Blue Points
excerpt: Given N distinct red and N distinct blue points on a 2D plane, no three of which are colinear, prove that there exists a way to connect (using line segments) each red point to a unique blue point such that no two line segments intersect.
math: true
---

We're back(!) with a problem given to us by our mathematical friend Phillip Lo, who encountered this question in a problem set. I thought my proof was pretty clean (partly because it took us about a month to finally get to it), but it turns that there are even cooler ones out there for us to enjoy.

### Q:

Given $$N$$ distinct red and $$N$$ distinct blue points on a 2D plane, no three of which are colinear, prove that there exists a way to connect (using line segments) each red point to a unique blue point such that no two line segments intersect.

### A:

Our first thought for problems like these is to just hit it with induction, and that's exactly what we'll do. We note that the $$N = 1$$ case is trivial, as we just connect the two points.

So now assume (for strong induction) that the theorem is true for all configurations of $$1, 2, \dots, N-1$$ pairs of points.

#### Lemma 1 (Bounding Polygon Lemma de Franklin Lu)

Consider the convex bounding polygon of the $$2N$$ points. (You can easily prove that a bounding polygon exists, e.g. take a large circle and shrink it and see what points it collapses onto first. There always exists a convex bounding polygon, since given a concave bounding polygon, you can just remove the concavity points and you'll have a convex bounding polygon left).

If the convex bounding polygon contains points of both colors, then we are done: there exists a valid nonintersecting connection configuration.

#### Proof Lemma 1

Since the bounding polygon contains points of both colors, it must contain a pair of adjacent points of different colors. Connect these two points. For the remaining $$N-1$$ pairs of points, by our inductive hypothesis, there exists a valid connection configuration. Since the two initial points are on the convex bounding polygon, their connecting line segment can't interfere with the connection configuration for the $N-1$ pairs of points. Thus we can trivially combine the two configurations to obtain a valid configuration for the $$N$$ pairs of points. $$\square$$

#### Lemma 2 (Infinite Rotations Lemma)

There exists a rotation of the plane such that no two points (of either color) lie on the same vertical line.

#### Proof Lemma 2

There are only finitely many pairs of points (and thus only finitely many possible connecting line segments), but there are infinitely many rotations of the plane. 

More rigorously, fix the plane and consider the set of all pairs of points. For each possible pair of points, compute the angle the line through the two points makes with with the $$x$$-axis. The resulting set of angles is finite, so there exists some angle $$\theta$$ such that for any angle $$\phi$$ in our set of angles,

\\[ \phi + \theta \not \equiv \frac{\pi}{2} \pmod{\pi} \\]

Rotate the plane by angle $$\theta$$. $$\square$$

#### Lemma 3 (Planar Splitting Lemma)

There exists a line that splits the $$2N$$ points such that there are exactly $$k$$ red points and $$k$$ blue points on one side of the line, and $$N-k$$ pairs of points on the other side of the line, for some $$k$$.

#### Proof Lemma 3

Suppose that the convex bounding polygon of the $$2N$$ points is uniformly colored (WLOG) blue.

By Lemma 2, we can find a rotation of the plane such that no two points lie on the same vertical line. Consider a vertical line that starts at the leftmost point and translates horizontally to the right. Define the function $$f(i)$$ to be the number of blue points left of the line minus the number of red points left of the line when the line is between the $$i$$th and $$i+1$$th points. This function is well defined, since no two points lie on the same vertical line.

Since the convex bounding polygon is uniformly blue, we note that $$f(1) = 1$$.

Also, after the rightmost point, $$f(2N) = 0$$, which implies that $$f(2N - 1) = -1$$, since the rightmost point is blue (since the bounding box is all blue).

Since $$f$$ only moves up and down in increments of $$1$$, the above implies that there must be some $$1 < i < 2N - 1$$ such that $$f(i) = 0$$. This gives us our desired splitting line. $$\square$$

#### Putting It All Together

By Lemma 1, if the convex bounding polygon of the points is nonuniformly colored, we are done.

If the bounding polygon is uniformly colored, then by Lemma 3, we can split the points into two sections, where one section has $$k$$ pairs of red and blue points, and the other section has $$n-k$$ pairs of red and blue points. By our inductive hypothesis, these two sections have valid connecting configurations. 

Since these two sections are separated by a line, their connections can't interfere with each other, thus we can combine them into a full configuration for the $$N$$ pairs of points. This completes the induction, which proves the original problem statement.

### One Alternative Proof

As an addendum, I present a really neat proof (and the classic textbook proof), which I think does this problem the best justice.

Suppose the two line segments $$AB$$ and $$CD$$ intersect at point $$X$$. Then by the triangle inequality, the sum of the lengths of the line segments $$AC + BD$$ is less than $$AB + CD$$, since

\\[ AC + BD < (AX + CX) + (BX + DX) = AB + CD \\]

This gives us the following algorithm: 

1. For any configuration of points, arbitrarily connect each red point to a unique blue point. 
2. If no connecting segments intersect, we are done.
3. Otherwise, take a pair of intersecting line segments (say, $$AB$$ and $$CD$$), connect $$AC$$ and $$BD$$, and erase the $$AB$$ and $$CD$$ connections.
4. Go to Step 2.

By our initial observation on swapping connections, we note that the sum of the lengths of all of the connecting line segments strictly decreases when we execute Step 3. But there are only finitely many connection configurations, so this sum cannot decrease forever, which means our algorithm must terminate at a local minimum eventually. When the algorithm has reached a local minimum, we are left with a valid connection configuration, since otherwise we could perform Step 3 again and further decrease the total length sum. $$\square$$
