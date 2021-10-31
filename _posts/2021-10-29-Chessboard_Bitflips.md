---
layout: post
author: John Zhao
title: "Chessboard Bitflips"
excerpt: Given a chessboard with an arbitrarily-flipped coin on each square, can I communicate a specific square on the board to you by flipping a single coin on the board?
math: true
date: 2021-10-29
---

I kinda have to comment on how I'm writing two posts in the span of seven days. I'd like to say that this spree will continue, but I'm actually kinda out of queued solved problems after this one. It's okay though, I'm sure I or someone else will solve something else at some point.

The problem I want to share today comes from one of my favorite YouTube channels, 3Blue1Brown. The channel has a few videos on exploring this problem, which you can find here: https://www.youtube.com/watch?v=wTJI_WuZSwE

### Q:

Players $$A$$ and $$B$$ are playing a game to win a prize.

There is a closed room with an 8x8 chessboard where each of the $$64$$ squares has exactly one coin placed on it. Each coin is showing either heads or tails. The prize is located under one of the squares of the board. Player $$A$$ enters the room and is made aware of which square holds the prize. He surveys the board state, and must flip exactly one coin. He then leaves the room, after which Player $$B$$ enters. $$B$$ surveys the new board state and must decide which square holds the prize.

(The orientation of the board is fixed, meaning that $$A$$ and $$B$$ can agree on which edge of the board is the "top" side)

Players $$A$$ and $$B$$ cannot communicate once the game has started. However, before the game begins, they are allowed to strategize together. Does there exist a strategy such that $$A$$ and $$B$$ are guaranteed to find the prize no matter what the initial configuration of coins?

### A:

Because the orientation of the board is fixed, we can index the squares on the board $$0, 1, 2, 3, ..., 63$$. Every board state can thus be encoded uniquely by a $$64$$-bit integer $$x$$, where the $$i$$th index of $$x$$ is $$1$$ if the $$i$$th square of the board state is showing heads, and $$0$$ if it is showing tails. In fact, it is easy to see that this mapping of board state to $$64$$-bit integer is bijective, since given any $$64$$-bit integer, we can generate a unique board state. Because of this bijection, I will refer to board states and their $$64$$-bit representations interchangeably.

We can restate the problem as follows: is there a strategy such that given any $$64$$-bit integer $$x$$ and any index $$i \in \{ 0, ..., 63 \}$$, Player $$A$$ can always flip a single bit of $$x$$ (yielding a new $$64$$-bit integer $$y$$) such that when $$B$$ sees $$y$$, he can determine the value of $$i$$?

Even more precisely, let's define the "bit flipping function" $$F(x,k) =$$ the result of flipping the $$k$$th bit of $$x$$.

The we can restate the problem as follows: do there exist functions $$I$$ and $$C$$ such that given any $$64$$-bit integer $$x$$ and any index $$i \in \{ 0, ..., 63 \}$$, we can guarantee
\\[ C(F(x, I(x,i))) = i \\]

We can think of the function
\\[ C: \\{ 0, ..., 2^{64} - 1 \\} \to \\{ 0, ..., 63 \\} \\]

as a *classification function* which classifies every possible board state into one of $$64$$ categories, with each category corresponding to a unique index on the board. When player $$B$$ sees the final board state, he can use $$C$$ to calculate the classification of the final board state, which will indicate the prize index.

We can think of the function
\\[ I: \\{ 0, ..., 2^{64} - 1 \\} \times \\{ 0, ..., 63 \\} \to \\{ 0, ..., 63 \\} \\]

as an *index identification function* which identifies the index of the bit we should flip in $$x$$ in order to transform $$x$$ into a board state whose classification is the prize index $$i$$ we desire. Player $$A$$ can use $$I$$ to identify which coin on the board he should flip such that the classification of the resulting board state corresponds to the prize index.

At this point, now that we have formalized what we are looking for, there are many ways to go about the problem. For example, we can think of the problem as a graph theory problem: we can view every possible board state as a node in a graph, and two board states have an edge between them iff they are exactly one bit flip apart. In fact, as noted by the 3Blue1Brown video, this is no ordinary graph; it is isomorphic to a $$64$$-dimensional (hyper)cube.

However, it turns out (unsurprisingly) that searching for this magical index identification function $$I(x,i)$$ is hard work. A lot of the difficulty comes from the fact that the domain of $$I(x,i)$$ is really huge. If you try to manually draw out the graph--even for the smaller 4x4 board--you'll find that the sheer number of board states is unmanageable.

We were stuck at this point for quite some time until Franklin Lu had the liberating idea to simplify the identification function $$I(x, i)$$ with some wishful thinking. Given a target prize index, instead of trying to map each individual board state to a bitflip index, what if we chose the bitflip index purely based on the category of the current board state? In other words, instead of looking for a function $$I(x,i)$$ where $$x$$ can take on $$2^{64}$$ values, let's search instead for a simpler function $$I_s(k, i)$$ where $$k = C(x)$$ and can only take on $$64$$ values.

This problem is a example of an interesting phenomenon in math where the harder version of a problem is actually easier to solve. In this case, note that any solution we find for $$I_s(k,i)$$ immediately yields a solution $$I(x,i) = I_s(C(x),i)$$, but clearly the reverse is not true. Finding $$I_s(k,i)$$ is a fundamentally harder problem than finding $$I(x,i)$$, but somehow--to our human brains--it is actually much easier to wrap our minds around.

Let's examine this simplified index identification function
\\[ I_s: \\{ 0, ..., 63 \\} \times \\{ 0, ..., 63 \\} \to \\{ 0, ..., 63 \\} \\]

Firstly, we note that $$I_s$$ is a bioperator on the set $$\{ 0, ..., 63 \}$$. As we shall soon see, using infix notation will neaten up a lot what we are about to write. Let's define, for $$k, i \in \{ 0, ..., 63 \}$$:
\\[ k \circ i = I_s(k,i) \\]

#### Observation

Suppose that we can find a bioperator $$\circ$$ which satisfies all of the following properties for all $$a,b,c \in \{ 0, ..., 63 \}$$:
1. associativity, i.e. $$ (a \circ b) \circ c = a \circ (b \circ c) $$,
1. commutativity, i.e. $$ a \circ b = b \circ a $$,
1. $$ a \circ 0 = a $$, and
1. $$ a \circ a = 0 $$.

Then we can use $$\circ$$ to build ourselves a winning strategy for the game.

#### Explanation of Observation

Given $$\circ$$, we can define $$C: \{ 0, ..., 2^{64} - 1 \} \to \{ 0, ..., 63 \}$$ as follows:
\\[ C(x) = x_0 \circ x_1 \circ x_2 \circ ... \circ x_{63} \\]

where $$x_n = n$$ iff the $$n$$th bit of $$x$$ is $$1$$, and otherwise $$x_n = 0$$. 

Recall that we defined the bitflipping function $$F(x,n)$$ as the result of flipping the $$n$$th bit of $$x$$.

Consider the expression $$C(F(x,n))$$, that is the categorization of $$x$$ after we flip its $$n$$th bit. There are two cases:

Case 1: the $$n$$th bit of $$x$$ is $$1$$. In this case, $$x_n = n$$. When we flip the $$n$$ bit of $$x$$, it'll become a $$0$$, which means that
\\[ C(F(x,n)) = x_0 \circ .... \circ x_{n-1} \circ x_{n+1} \circ ... \circ x_63 \\]

Because $$\circ$$ satisfies the properties (3) and (4) listed above, we can add in $$0 = n \circ n = x_n \circ n$$ to the RHS of the equation without changing its value. By associativity and commutativity of $$\circ$$, we are free to rearrange the terms in the chain of $$\circ$$ applications, which leaves us with

\\[ C(F(x,n) = x_0 \circ .... \circ x_{n-1} \circ x_n \circ x_{n+1} \circ ... \circ x_63 \circ n \\]
\\[ \implies C(F(x,n)) = C(x) \circ n \\]

Case 2: the $$n$$th bit of $$x$$ is $$0$$. In this case $$x_n = 0$$. When we flip the $$n$$th bit of $$x$$, it'll become a $$1$$, which means that
\\[ C(F(x,n)) = x_0 \circ ... \circ x_{n-1} \circ n \circ x_{n+1} \circ ... \circ x_63 \\]
\\[ = x_0 \circ ... \circ x_{n-1} \circ x_n \circ x_{n+1} \circ ... \circ x_63 \circ n \\]

Here we moved the $$n$$ term to the end, and we added in an extra $$x_n$$ since $$x_n = 0$$. We observe once again that
\\[ C(F(x,n)) = C(x) \circ n \\]

Since this equality holds for both cases, it holds generally. 

Let's define our bitflip index identification function as follows:
\\[ I(x,i) = I_s(C(x),i) = C(x) \circ i \\]

As noted before, to show that our strategy works, we just need to show that for all $$x \in \{ 0, ..., 2^{64} - 1\}$$ and all $$i \in \{ 0, ..., 63 \}$$,
\\[ C(F(x,I(x,i))) = i \\]

Noting our above derivations, we have:
\\[ C(F(x,I(x,i))) = C(x) \circ I(x,i) \\]
\\[ = C(x) \circ C(x) \circ i \\]
\\[ = i \\]

which is exactly what we wanted. Thus we have defined two functions $$C,I$$ which yield a guaranteed winning strategy for the game!

#### Does $$\circ$$ Exist?

It remains to show that an operator $$\circ$$ satisfying the four properties listed above actually exists.

Although group theory is definitely not a requirement for solving this problem, those of you who are familiar with group theory will note that finding $$\circ$$ is equivalent to showing that there exists a *commutative group* $$(G, \circ)$$ of size $$64$$ such that for any elements $$a,b \in G$$,
\\[ a \circ b = 0 \\]
where $$0$$ is the identity element of the group. 

In fact this group theoretic approach was the approach that I went with when I initially solved the problem. It is possible to explicitly generate a group with the properties above. Consider the group generated by the following set of independent cyclic 2-permutations: $$ \{ (1,2), (3,4), (5,6), (7,8), (9,10), (11,12) \} $$. It is relatively simple to show that this group is commutative (since the elements in the generating set are all independent of each other), that any element of the group is its own inverse (since applying the same cyclic 2-permutation twice will yield the identity permutation), and that it has size $$64$$ (since any element in the group is uniquely determined by which cyclic 2-permutations of the generating set it contains, which means there are $$2^6 = 64$$ total elements).

In this way the problem is essentially solved; however, there is an even nicer way of representing the operator $$\circ$$. We note that the $$XOR$$ operator actually satisfies all of the properties of $$\circ$$! This makes a lot sense when thinking about the group that we constructed: we can draw a one-to-one mapping between group elements and $$6$$-bit integers, where the $$n$$th index of an integer represents whether or not the group element contains the $$n$$th cyclic 2-permutation in the generating set, i.e. whether it contains $$(2n+1,2n+2)$$. Since cyclic 2-permutations cancel themselves out when composed with themselves, composing two elements of the group is equivalent to $$XOR$$ing their corresponding integer representations.

#### Putting It All Together

Let's summarize our results into a full strategy for the game.

We define the *classification function*
\\[ C(x) = x_0 ~XOR~ x_1 ~XOR~ x_2 ~XOR~ ... ~XOR~ x_{63} \\]

where $$x$$ is a board state, and

$$x_n = n$$ if the $$n$$th square of the $$x$$ is showing heads, otherwise

$$x_n = 0$$.

At the start of the game, Player $$A$$ enters the room where he is given the index $$i$$ of the prize square, and he also observes the initial board state $$x$$. He computes $$C(x)$$, the initial categorization of the board. He then computes the board index $$k$$ that he should flip: $$k = C(x) ~XOR~ i$$. He then flips the coin on the $$k$$th index of the board, yielding an updated board state $$F(x,k)$$.

Player $$B$$ enters the room can computes the categorization of the updated board state $$C(F(x,k))$$. By our analysis above, $$B$$ can be confident that
\\[ C(F(x,k)) = C(x) ~XOR~ k \\]

\\[ = C(x) ~XOR~ C(x) ~XOR~ i \\]

\\[ = i \\]

the index of the prize square.
