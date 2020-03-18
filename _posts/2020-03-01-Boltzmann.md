---
layout: post
author: Frimpong Baidoo
title: Boltzmann's theorem (for lack of a better name)
excerpt: We prove a theorem with implications for conservation of mass, momentum and energy in kinetic theory. 
math: true
---

### Q: Let $$\eta$$ be some unit vector and $$v_1$$ and $$v_2$$ be arbitrary vectors in $\mathbb{R}^D$ ($$D > 1$$) and define \\[ v_1' = v_1 - ( (v_1 - v_2)\cdot\eta)\eta \\] \\[ v_2' = v_2 + ( (v_1 - v_2)\cdot\eta)\eta \\]
If $\varphi(v)$ is a $C^2$-function such that $\varphi(v_1) + \varphi(v_2) = \varphi(v_1') + \varphi(v_2')$ for all choices of $\eta$, $v_1$ and $v_2$, then \\[ \varphi(v) = A + B\cdot v + C|v|^2 \\]


(_Remark 1_): $v_1'$ and $v_2'$ are the velocities of two equal mass balls (or billiards or whatever floats your boat at the moment) after they undergo an elastic collision with initial velocities $v_1$ and $v_2$. Thus the above identity in $\varphi(v)$ tells us that the only conserved quantities in an elastic collision are mass ($\varphi(v) = 1$), momentum ($\varphi(v) = v$) and energy ($\varphi(v) = \|v\|^2$).
 
(_Remark 2_): This result was first proved by Boltzmann (circa 1890) but this particular proof is my elaboration on one from an as yet unpublished manuscript of Dr. Irene Gamba.

### A:	A straightforward computation would verify that
$$\begin{align} &(1) \qquad \,v_1 + v_2 = v_1' + v_2' \\ &(2)\qquad |v_1|^2 +|v_2|^2= |v_1'|^2 +|v_2'|^2  \end{align} $$

We define 

$$ \begin{align} (3)\qquad w = \frac{v_1 + v_2}{2} = \frac{v_1' +v_2'}{2} \end{align} $$ 

and observe that \\[ v_1 = w + u \,;\quad v_2 = w - u\\] \\[ v_1' = w + y \,;\quad v_2' = w - y \\] where $\,u = (v_1-v_2)/2\,$ and $\,y = (v_1' -v_2')/2$. 

Furthermore through (2), we see that $\|y\| = \|u\| $. Thus by assumption, for all vectors $u$ and $y$ of equal length, $\varphi(v)$ will be such that \\[ \varphi(w +u) + \varphi(w-u) = \varphi(w+y) + \varphi(w-y)\\]
This means that 

\\[ \frac{\varphi(w +u) + \varphi(w-u) - 2\varphi(w)}{\|u\|^2}\, = \, \frac{\varphi(w+y) + \varphi(w-y) - 2\varphi(w)}{\|y\|^2} \\] 

and by taking the limit where $\|u\| = \| y\|$ goes to zero, we get (via Taylor series expansions of $\varphi(w\pm u)$ ) \\[\hat{u}^T H_\varphi(w)\hat{u} = \hat{y}^T H_\varphi(w)\hat{y}  \\] 
where $H_\varphi(w)$ is the Hessian of $\varphi$ at $w$ and $\hat{u}$ and $\hat{y}$ are the unit vectors in the direction of $u$ and $y$ respectively. This applies to any choice of unit vectors $\hat{u}$ and $\hat{y}$ because $v_1$, $v_2$ and $\eta$ can be chosen arbitrarily. In particular, it will apply to the standard basis of $\mathbb{R}^D$ \\[\hat{e_i}^{T} H_\varphi(w)\hat{e_i} = \hat{e_j}^T H_\varphi(w)\hat{e_j}  \\] 
By picking $\hat{u} = \frac{\hat{e_i}-\hat{e_j}}{\sqrt{2}}$ and $\hat{y} = \frac{\hat{e_i} + \hat{e_j}}{\sqrt{2}}$, we also find that the off-diagonal terms of the Hessian matrix are zero. This means that the Hessian matrix is a scalar multiple of the identity matrix: $$H_{\varphi}(v) = 2C(v)\,\mathbf{Id}_{D} $$. 

As a result of the Hessian having zero off-diagonal terms, $\varphi(v)$ takes the form \\[ \varphi(v) = \sum_{i=1}^D f_i(v_i) \\] whilst the diagonal terms of the Hessian lead to the equality $$\partial_{ii}f_i(v_i) = 2 C(v) = \partial_{jj}f_j(v_j) $$ which is only possible if $C(v)$ is constant. Thus $\varphi(v)$ is a sum of quadratic polynomials $$ f_i(v_i) = a_i + B_i v_i + C v_i^2$$ or equivalently 

\\[ \varphi(v) =  A + B\cdot v + C\|v\|^2\\]

<div style="text-align: right"> $\blacksquare$ </div>

(_Remark 3_): The theorem is still true even if $\varphi$ is a distribution (also called a [generalised function](https://mathworld.wolfram.com/GeneralizedFunction.html)). The proof involves convolving $\varphi$ with a sequence of smooth, compactly-supported functions that converge to the dirac delta distribution. We then use the above proof to argue that the convolved function takes the expected form and that this form is maintained in the limit.














