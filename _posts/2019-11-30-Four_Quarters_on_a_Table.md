---
layout: post
author: Franklin Lu
title: Four Coins on a Table
excerpt: You have 4 coins sitting at the four corners of a table. They are set to heads or tails randomly, and you are blindfolded. Your goal is to try to get all the coins to be on heads, after which the game immediately ends. The catch is that after each round, the table rotates by 90, 180, 270, or 360 at random. How do you win this game?
date: 2019-11-30
math: true
---
It has been a decently long time since my last blog post. Work has been busy, and the time that I do not spend working, I find I tend to really want to throw away to mindless activity. Anyways, there is a riddle as follows:

You have 4 coins sitting at the four corners of a table. They are set to heads or tails randomly, and you are blindfolded. Your goal is to try to get all the coins to be on heads, after which the game immediately ends. The catch is that after each round, the table rotates by 90, 180, 270, or 360 at random. How do you win this game?

In some sense, you have only four possible plays:

$$A$$: Flip a corner coin

$$B$$: Flip two coins on the same side

$$C$$: Flip two coins on a diagonal

$$D$$: Flip all coins 

Any other actions you can take are the same up to rotation (which shouldn't matter -- once the table starts turning you lose track of which orientation it was previously in, so your strategy should not depend on rotation), or the same after flipping all coins (this just covers the case where we flip three coins, which we realize is the same as flipping one. The last play, which is to flip all the coins, is just a way to check if you previously had all tails. In fact we can do a quick sanity check to make sure we are covering all possibilities: there are $$2^4 = 16$$ ways to flip the coins on the board, and there are 4 corners to play $$A$$ and for corners to play "not $$A$$" (by flipping all coins but the corner coin), 4 sides to play $$B$$, 2 diagonals to play $$C$$, and 1 way to play $$D$$. That brings us to 15 total ways to flip, with the final one being the choice to not flip any coins at all. Next, we would like to examine different board states, which look essentially identical to the ways to flip:

$$1$$: Corner coin is H, rest are T

$$2$$: Two coins on the same side are H, rest are T

$$3$$: Two coins on the diagonal are H, rest are T

$$4$$: All coins are H

Again, there are other board states, but they are obtained by rotating these board states or flipping all coins from one of these board states. We now want to see how each play acts on board states.

Playing $$A$$ sends:

$$1 \rightarrow 2,3,4 $$

$$2 \rightarrow 1 $$

$$3 \rightarrow 4 $$

Playing $$B$$ sends:

$$1 \rightarrow 1 $$

$$2 \rightarrow 3,4 $$

$$3 \rightarrow 2 $$

Playing $$C$$ sends:

$$1 \rightarrow 1 $$

$$2 \rightarrow 2 $$

$$3 \rightarrow 4 $$

I have omitted board state 4, because the game ends when we reach board state four (or if we have all tails, we simply flip all coins). I have also omitted play D, because it does nothing to the board state (we still will use it after each flip, to check if we were in an all tails board). We solve by inspection.

First, we notice that we should be playing D every other round (and the first round) to ensure that we don't accidentally pass over a board state 4 in all tails and miss out on a win. Next, we notice that playing C on either 1 or 2 sends us back to 1 or 2, and playing C on board 3 sends us to board 4. So we can play C freely to check for board 3, and we do. So now we know that playing DCD is a win from board 3, and otherwise leaves the game unchanged. Our problem is simple enough that we can just do the rest, but we can also update our table:

Playing $$A$$(then $$DCD$$) sends:

$$1 \rightarrow 2,3 $$

$$2 \rightarrow 1 $$

Playing $$B$$(then $$DCD$$) sends:

$$1 \rightarrow 1 $$

$$2 \rightarrow 3 $$

From here, it becomes clear that playing B sends state 1 back to itself, and it sends state 2 to state 3, which is a win (after playing DCD), so we know that BDCD wins from state 2 and does nothing to state 1, so we can play that safely here. Then, if the game is still going, we are in state 1. We play A, which sends us to 2 OR 3, after which we play DCD to check for 3, and if the game continues, then we play BDCD to win from state two, which gives us our final answer.

DCD (checking for 3)

BDCD (checking for 2)

A (moving from 1)

DCD (checking for 3)

BDCD (checking for 2)

As a final note, there is something interesting about this problem, and I do wonder if there are any interesting extensions. There is something very algorithmic about shrinking the states you can be in, while each string of plays corresponds to a certain board state that you can check for (while leaving others untouched). I wonder if something like a 3x3 board or a 4x4 board could be similarly solved. I also wonder if boards with even numbers of coins can be solved more easily, given that the number of heads and tails will always be both even or both odd.