---
layout: post
author: Franklin Lu
title: The Lu-Zhao Conjecture
excerpt: JZ once asked us -- myself, Kevin, and Jeff, that is -- a now classic riddle. Given a balance and 3 uses of said balance, how can you always find the bad apple out of thirteen apples? The bad apple weighs slightly more, or slightly less, but you do not know which.
date: 2018-09-11
math: true
---
Not all solutions will be like this, but this is also a blog, which means sometimes they will be like this. That is, not just a solution, but a history of the problem, and the solution, and general thoughts about why math things are good.

JZ once asked us -- myself, Kevin, and Jeff, that is -- a now classic riddle. Given a balance and 3 uses of said balance, how can you always find the bad apple out of thirteen apples? The bad apple weighs slightly more, or slightly less, but you do not know which.

This is already a hard riddle, but it really just amounts to playing with the apples and trying to make sense of a very finite number of things. There are a lot of ideas that help you get to good ideas, and because the search space are small, these good ideas are right ideas a lot of the time. For example, for the first weighing, you might try 3-3 or 5-5, but in the 3-3 case you realize you get left with 7 in 2 weighs if they balance, and that seems hard. And if 5-5 tips, well you have 10 apples in two weighs, which is also seems hard. So you can "prove" that the first weighing is 4-4, and you can play with it until you get it. The rest of the solution can be reached without too much difficulty, if you spend long enough.

Steven Cooklev once mentioned a solution he read about. He claimed that each weighing did not depend on the outcome of the previous one. JZ and I attempted to recreate such a solution, and I think we proved it was impossible (we really tried a lot of stuff). But the article was based on the idea that each weighing provided three outcomes: $$-1$$ (tip left), $$0$$ (balance), $$+1$$ (tip right), which meant that the outcomes could maybe index $$3^3 = 27$$ apples. But there's also some fudge factor, so you divide by two (something about symmetry, I don't really know). And you get $$13.5$$, which means you can find $$1$$ apple out of $$13.5$$ apples in $$3$$ weighs. What is the $$.5$$? I don't know -- some speculation about how maybe a mythical 14th apple could be added to the problem was something we discussed. But 13 apples seemed like a hard limit from what we saw, and I think we just decided to round down and so we ended up getting the now famous Lu-Zhao Conjecture:

In $$N$$ weighings with a balance, you can find a bad apple from $$\frac{3^N - 1}{2}$$ apples.

We sought to prove this, and in hindsight I guess it wasn't too hard. But it was a good exercise in induction and also just a good thing to get excited about. There was a little bit of that feeling that mathematicians probably get when they actually prove a real noteworthy conjecture, when they do some real math.

Anyways, the proof:

### Lemma:
If you know if the bad apples is heavier or lighter, you can find the bad apple from $$3^N$$ apples for $$N$$ weighings.

### Proof:
In the base case, you have three apples. WLOG assume two heavy (by pidgeonhole you double up on either heavy or light). You weigh two heavy against each other, if they balance it is the omitted, if they tip it is the heavier one (because you only have potentially heavy bad apples).

If you have $$3^N$$ apples, split them into groups of three. Assume the bad is heavy. Then you have groups of $$3^{N - 1}$$, and you can tell if the apple is one of those three (if balance, then it is omitted group, and if tip, then it is heavy group). So you use one weighing, and have $$N - 1$$ left, with $$3^{N - 1}$$ apples left.

### Lemma:
If you have sufficient good apples, then you can find a bad apple out of $$\frac{3^N + 1}{2}$$ for $$N$$ weighings.

### Proof:
Base case: you have $$N = 1$$. So you have $$2$$ total apples, and you have your reference apples. Just do it.
Now, assuming you can do $$\frac{3^k + 1}{2}$$ in $$k$$ weighings, we show that the $$k+1$$ case holds. With $$\frac{3^{k+1} +1}{2}$$ apples, and we set aside $$\frac{3^k + 1}{2}$$ of the apples, and weigh the other $$3^k$$ against reference. We are left with two cases: when $$3^k$$ tips against the good apples, we know their heavy/lightness, and we use the above lemma, and when the $$3^k$$ apples balance against the good apples, then we have $$\frac{3^k + 1}{2}$$ in $$k$$ weighings, with plenty of reference apples, which is the $$k$$-case.

Now, we can finally move on to the main part of the proof. Assuming the k-case holds, and using the $$13$$ apple case as the base case, we try to prove the $$k+1$$ case.

Separate our $$\frac{3^{k+1} -1}{2}$$ apples into $$3$$ groups: $$2$$ groups of $$\frac{3^k - 1}{2}$$, and $$1$$ group of $$\frac{3^k + 1}{2}$$. Then, we weigh the first two against each other. If they balance, then we have plenty of reference apples, and we just apply the second lemma. If they don't balance, things get a little bit tricky.

When they do not balance, we have $$\frac{3^k - 1}{2}$$ heavy apples and the same number of light apples. We also bear in mind that we have access to $$\frac{3^k + 1}{2}$$ good apples. We then proceed as follows:

Put $$3^{k-1}$$ light apples and $$\frac{3^{k-1} - 1}{2}$$ heavy apples on one side, and $$\frac{3^{k-1} - 1}{2}$$ light apples and $$3^{k-1}$$ good apples on the other side. Notice we have enough reference apples, and we have placed all our light apples, leaving off $$3^{k-1}$$ heavy apples to the side. Now, there are three cases:

If this balances, we know the apple must be in $$3^{k-1}$$ heavy apples, which we can find in $$k-1$$ weighings.

If the mixed side tips up, we know that the bad apple must be in the light apples on the mixed side, and so we can find the apple out of $$3^{k-1}$$ light apples in $$k-1$$ weighings.

If the mixed side tips down, we have $$\frac{3^{k-1}}{2}$$ heavy apples and $$\frac{3^{k-1}}{2}$$ light apples. This, notice, is the $$k$$ case of this algorithm itself, where we have just performed an initial weighing and the balance has tipped. So by induction, this is also solved. This completes the proof.

The hardest part of the proof was the last step, with the mixing of heavy/light apples. The idea came to me as I was sitting in the CCUC pews, perhaps dozing off a little. But it does make a lot of sense, especially when you split it up into cases where you know how to handle -- with information, with reference, etc.