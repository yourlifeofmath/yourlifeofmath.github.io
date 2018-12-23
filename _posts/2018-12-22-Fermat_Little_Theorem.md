---
layout: post
author: John Zhao
title: A Little Proof of Fermat's Little Theorem
excerpt: A quick neat proof of Fermat's Little Theorem using basic modular arithmetic. Also, welcome to the new website!
math: true
---
As a non-mathematical aside, we have migrated the blog from Blogspot to Github Pages, which is now hosting our own static website built using `Jekyll`. Hopefully, we will no longer have to resort to uploading pdf's of compiled Latex in order to achieve satisfactory levels of mathematical aesthetics.

### Q:
Prove that for any integer $$a$$ and any prime number $$p$$,

\\[ a^p \equiv a \pmod p \\]

### A:
The question above is a brief restatement of Fermat's Little Theorem, a famous result in number theory. Not to be confused with Fermat's Last Theorem, this little theorem is actually much easier to prove, as can be seen by the plethora of [proofs](https://en.wikipedia.org/wiki/Fermat%27s_little_theorem) found on Wikipedia, etc. One interpretation of this theorem is that the number $$a^p - a$$ is always a multiple of $$p$$, a fact that is not inherently obvious.

Our approach to proving the theorem is through the use of a fact known commonly as the "Freshman Binomial Theorem," which states that for all prime $$p$$,

\\[ {(x + y)}^p \equiv x^p + y^p \pmod p \\]

The reason for the name of the theorem is that it would be a "freshman's dream" to be able to expand binomial powers ignoring the middle terms.

Proving this theorem is simple using the actual Binomial Theorem. We expand $${(x + y)}^p$$, which yields

\\[ x^p + {p \choose 1} x^{p-1}y + {p \choose 2} x^{p-2}y^2 + \cdots + {p \choose p-1} xy^{p-1} + y^p \\]

Each binomial coefficient can be written

\\[ {p \choose k} = \frac{p \cdot (p-1) \cdot (p-2) \cdots (p - k + 1)}{k!} \\]

and since $$p$$ is prime and $$k < p$$, none of the factors in the denominator will cancel out the $$p$$ in the numerator, which implies that each of the binomial coefficients is divisible by $$p$$, which means that $$\pmod p$$ we can safely ignore all the middle terms, and we are left with the original statement of the Freshman Binomial Theorem:

\\[ {(x + y)}^p \equiv x^p + y^p \pmod p \\]

With this tool in hand, proving Fermat's Little Theorem is a matter of simple induction. We note that trivially,

\\[ 1^p \equiv 1 \pmod p \\]

Assume for induction that

\\[ k^p \equiv k \pmod p \\]

Then, using the Freshman Binomial Theorem and our inductive hypothesis, we have

\\[ {(k+1)}^p \equiv k^p + 1^p \equiv k + 1 \pmod p \\]

and thus the induction is complete. $$\square$$