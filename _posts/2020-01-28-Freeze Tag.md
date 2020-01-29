---
layout: post
author: Franklin Lu
title: "Freeze Tag"
excerpt: At long last, the Riddler problem from over two years ago. Freeze tag!
math: true
date: 2020-01-28
---

Taken from the Jun 16th, 2017 Riddler:

A group of $$n$$ players play a game of tag. Each player is equally likely to tag any other player. When a player is tagged, they sit down, and when the player that tags them sits down, they rejoin the game. How long, in tags, is this game expected to last?

John and I first saw this problem in college, and over the past few years we've worked on it on and off. I forget when we started calling it "Freeze Tag", but that is the name that stuck. When we first encountered the problem, a lot of the other problems we had been doing were simple Markov chain riddles. None of those techniques worked -- this problem is significantly harder. We weren't sure there even was a simple answer, as sometimes The Riddler will post problems that require simulation to solve.

Over a few years, working on other problems on and off (and really, just going through life -- three years is long time), this problem would find itself in the background. Too hard to seriously work on, but tractable and with a seemingly elegant solution to be uncovered which forced us never to truly give up on it. Now, at long last, we have a solution.

Obviously, when trying this problem, the first thing is to try all the small cases.

In the smallest case, $$n=2$$, we have that the expected time is $$1$$.

For $$n=3$$, the expected time is $$3$$. Again, a relatively simple Markov chain. We start in the state of three single players, and with probability one, one player tags another. Call this state $$X$$. From $$X$$, half the time we choose the same tagger and the game ends, and the other half of the time we choose the other player to tag, which means now that player forms a group of two, and the tagger player rejoins the game -- returning to $$X$$. And so we have, $$E[X] = \frac{1}{2}(E[X] + 1) + \frac{1}{2}(1)$$, and so $$X = 2$$, and so the total expected time is $$3$$.

Following similar logic, $$n = 4$$ has an expected time of $$7$$.

For $$n>4$$, it becomes harder and harder to find the solution as the number of states begins to grow quickly, and keeping track of all the states and transition probabilities becomes a nightmare. But, by now, we already see a pattern begin to form. We can check $$n=5$$ with some effort, and once we verify that it has expected time 15, we should conjecture:

CONJECTURE 1: The expected time of the game is $$2^{n-1} -1$$.

Now, even with this in mind, we still could not make any progress on the problem. But it was promising -- such a tidy answer should have at least a reasonably tidy solution.

A few months ago, I redrew $$n=4$$ and began to consider, instead of expected time for the whole game, the expected time spent in each state. (A state here is a configuration of groups of remaining players and those they have tagged, with a state like $$(1,2)$$ representing a single player and a player who has tagged a second player. For example, $$n=4$$ has $$5$$ states: $$(1,1,1,1)$$, $$(1,1,2)$$, $$(1,3)$$, $$(4)$$, and $$(2,2)$$). This proved to be interesting for a number of reasons. For starters, it allows us to find the expected time for any state if we know the expected times of states that feed into that state. Let us make that more clear here:

REMARK: For a state $$X$$, the time spent in that state is given by $$\mathbb{E}[X] = \sum p(i)\mathbb{E}[X_i]$$, where $$p(i)$$ is the transition probability from source state $$X_i$$ into state $$X$$.

This allows us to make some interesting observations. First, one minor point, let us define the expected time in state $$(n)$$ to be $$1$$. Normally it would be $$0$$, because the game ends before we spend any time there, but it doesn't change anything else about the problem. Because we know that the time spent in the state $$(n)$$ is $$1$$, and the state $$(1, n-1)$$ always enters $$(n)$$ with probability $$p = \frac{1}{2}$$, we know that we must therefore spend on average $$2$$ tags in the state $$(1, n-1)$$. This fact seems interesting but is largely useless. But it is minorly useful as an example of another conjecture, which would end up reformulating the problem. First, we need to define a new term.

DEFINITION: The $$\textit{multiplicity}$$, $$m$$, of a state is defined as the number of arrangements of that state (order matters). For example, the state $$(1,2,3)$$ has multiplicity 6, which comes from the arrangements: $$(1,2,3), (1,3,2), (2,1,3), (2,3,1), (3,1,2), (3,2,1)$$.

One thing I noticed was that, in general, the expected time per state was equal to its multiplicity. It proved true for all the cases I could draw below $$n=5$$, which had me very interested.

REMARK (Useless): The multiplicity of a state $$(N_1, N_2...N_n)$$, where $$N_i$$ denotes the number of groups of size $$i$$, is given by $$\frac{(\sum N_i)!}{(\prod N_i)!}$$. 

PROOF: We can pretty easily prove this: the numerator is the way to arrange $$\sum N_i$$ elements and the denominator is to account for the ways we have overcounted arrangements within the 1's, 2's, ..., n's.

When I discovered the above fact, it seemed like it would be useful in perhaps some more explicit computations involving transition probabilities. Turns out it isn't, as most computations involving factorials quickly get out of hand. They might eventually reduce to expressions I want, but most of that kind of computation was not very fruitful.

REMARK (Extremely Useful): The sum of multiplicities across all states is equal to $$2^{n-1}$$.

PROOF: There is a very simple, very elegant proof that uses no mathematical identities, instead observing only a simple fact. Across all states, the sum of all multiplicities corresponds to the total number of arrangements where order matters. This, for $$n$$ players, corresponds to placing or not placing a divider between each of the players, or placing or not placing dividers in $$n-1$$ slots. Obviously, with two modes, divider on and divider off, the total number is $$2^{n-1}$$.

CONJECTURE 2: The expected time spent in each state is equal to its multiplicity.

I had already mentioned that this was a thought, but I write it again as something to be proven because the previous remark shows that Conjecture 2 $$\implies$$ Conjecture 1, with the discrepancy of the $$-1$$ term coming from the fact that, as we noted earlier, the game technically ends before we spend any time in the final state which has multiplicity 1.

Now, all we have to do is prove our new conjecture.

At this point, I didn't know exactly why multiplicity was so important. Turns out, there really is one reason. Each possible arrangement of a state corresponds to a way to simulate a tag from that state. In other words, instead of choosing a random tagger and a random taggee, we instead choose a random arrangement of the state and have a prearranged tagging take place. There are many ways to choose this tagging, but the way I originally came up with and stick to is: First Tags Last. Each of the $$m$$ arrangements of a state correspond to a way to exit that state.

I thought I was close here, but I really wanted to count the ways to enter a state. The reason for that was because, I figured if we had ways to enter a state, we could potentially induct from a source state, showing that, as we moved along towards the final state, each state along the way could be shown to have expected time spent equal to its own multiplicity.

Turns out, there are also $$m$$ ways to enter a state with multiplicity $$m$$. This fact wasn't immediately obvious given my tagging algorithm, as there was a bit of a catch. Consider the state $$(1,2,3)$$. Where does it come from? Well, it comes from a number of arrangements, but notably it comes from $$(1,3,1,1)$$ and $$(1,3,2)$$. In the case of $$(1,3,1,1)$$, first tags last and we get $$(2,3,1)$$. In the case of $$(1,3,2)$$, first tags last, and we ... also get $$(2,3,1)$$? I thought this was strange, and I realized that I had not accounted for what happens to any 1's coming out. I modified the tagging algorithm to account for this; First Tags Last and 1's in front. (The 1's in front account for the fact that, if first tags last and first always increases, the arrangements with 1's in front must have come from somewhere, in this case from a state where those 1's rejoined the game from a larger group).This way $$(1,3,2)$$ maps to $$(1,2,3)$$ and $$(1,3,1,1)$$ maps to $$(2,3,1)$$, and in general each arrangement came from exactly one other.

With this, we are very close to done. There are $$m$$ ways to enter a state and $$m$$ ways to exit it, and if every state has expected time equal to $$m$$, then it must be that each way to exit carries $$\frac{1}{m} * m = 1$$ unit of expected value to another state, and by similar argument receives 1 unit of expected value for each of $$m$$ ways of entering that state. This shows that Conjecture 2 is at least self-consistent. I thought I would need an induction to help complete the proof, but turns out consistency with itself is all we need.

REMARK: There is only one solution to the expected time per state.

PROOF: This is done by noting that, given a total of $$k$$ total states, each state uses comes from some linear combination of source states. This gives us $$k$$ unique equations and $$k$$ unknowns, which means that our solution is THE solution. Alternatively, we can also appeal to the Markov property of the problem and argue that there can only be one value for the expected time per state.

With that, having shown our solution is the only solution, we prove our original conjecture -- that the total time spent in the game is $$2^{n-1}$$.
