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

\begin{array}{ | c | c |}
\hline
FLIP & STAY \\
\hline
STAY & STAY \\  
\hline
\end{array}

\begin{array}{| c | c |}
\hline
FLIP & FLIP \\
\hline
STAY & STAY \\
\hline
\end{array}

\begin{array}{| c | c |}
\hline
FLIP & STAY \\
\hline
STAY & FLIP \\
\hline
\end{array}

\begin{array}{| c | c |}
\hline
FLIP & FLIP \\
\hline
FLIP & FLIP \\
\hline
\end{array}

Any other actions you can take are the same up to rotation (which shouldn't matter -- once the table starts turning you lose track of which orientation it was previously in, so your strategy should not depend on rotation), and obviously flipping one coin in the corner is the same as flipping the other three. The last play, which is to flip all the coins, is just a way to check if you previously had all tails. Next, we would like to examine different board states:


\begin{array}{ | c | c |}
\hline
H & T \\
\hline
T & T \\  
\hline
\end{array}

\begin{array}{| c | c |}
\hline
H & H \\
\hline
T & T \\
\hline
\end{array}

\begin{array}{| c | c |}
\hline
H & T \\
\hline
T & H\\
\hline
\end{array}

\begin{array}{| c | c |}
\hline
H & H \\
\hline
H & H \\
\hline
\end{array}

Again, there are other board states, but they are obtained by rotating these board states or flipping all coins from one of these board states. We now want to see how each play acts on board states. Label the plays A-D and the board states 1-4, and we have the following table:

\begin{array}{ | c | c | c | c |}
\hline
& 1 & 2 & 3 \\
\hline
A & 2,3,4 & 1 & 1 \\
\hline
B & 1 & 3, 4 & 2 \\
\hline
C & 1 & 2 & 4 \\
\hline
\end{array}

I have omitted board state 4, because the game ends when we reach board state four (or if we have all tails, we simply flip all coins). I have also omitted play D, because it does nothing to the board state (we still will use it after each flip, to check if we were in an all tails board). Other than that, the way to read the table is, for example, to look at the top left cell and see that, if we are in board state 1, playing A will send us to 2, 3, or 4. Now, we simply inspect the table for the solution.

First, we notice that we should be playing D every other round (and the first round) to ensure that we don't accidentally pass over a board state 4 in all tails and miss out on a win. Next, we notice that playing C on either 1 or 2 sends us back to 1 or 2, and playing C on board 3 sends us to board 4. So we can play C freely to check for board 3, and we do. So now we know that playing DCD is a win from board 3, and otherwise leaves the game unchanged. Our problem is simple enough that we can just do the rest, but we can also update our table:

\begin{array}{ | c | c | c |}
\hline
& 1 & 2 \\
\hline
A & 2,3 & 1 \\
\hline
B & 1 & 3 \\
\hline
\end{array}


Knowing DCD is a win from both 3 and 4, I have combined 3 and 4 into one state, 3. From here, it becomes clear that playing B sends state 1 back to itself, and it sends state 2 to state 3, which is a win (after playing DCD), so we know that BDCD wins from state 2 and does nothing to state 1, so we can play that safely here. Then, if the game is still going, we are in state 1. We play A, which sends us to 2 OR 3, after which we play DCD to check for 3, and if the game continues, then we play BDCD to win from state two, which gives us our final answer.

DCD (checking for 3)

BDCD (checking for 2)

A (moving from 1)

DCD (checking for 3)

BDCD (checking for 2)

As a final note, there is something interesting about this problem, and I do wonder if there are any interesting extensions. There is something very algorithmic about shrinking the states you can be in, while each string of plays corresponds to a certain board state that you can check for (while leaving others untouched). I wonder if something like a 3x3 board or a 4x4 board could be similarly solved.