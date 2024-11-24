---
title: "Optimal Code Existence for Countably Infinite Sources"
date: 2024-03-30T14:31:55-04:00
draft: false
---

Huffman coding demonstrates the existence and a concrete construction for
sources with finite alphabet. However, the construction fails when it comes to
infinity. We would prove the existence of the optimal code for sources with a
countably infinite alphabet.

# Notations

We only use 0 and 1 to construct codewords without loss of generality and the
base of $\log$ is 2 by default.

$X$ is the random variable from the source whose probability distribution is
$p_1 , p_2 , p_3 , \cdots$. And $l_1, l_2, l_3 \cdots$ denote the lengths of the
corresponding codewords. Without loss of generality, we make $p_1 \geq p_2 \geq
p_3 \geq \cdots$. By the [rearrangement
inequality](https://en.wikipedia.org/wiki/Rearrangement_inequality), we may set
$l_1 \leq l_2 \leq l_3 \cdots$. The problem we are considering here can be
modeled as an integer optimization problem:
$$
\text{Minimize} \quad \sum_{i=1}^\infty p_il_i \\
\text{s.t.} \quad \sum_{i=1}^\infty 2^{-l_i}\leq1
$$
using the extended Kraft–McMillan inequality for countably infinite sources.

Note that the bounded sum of $p$'s does not garantee the bounded sum of $p\log
p$'s. For example, set $p_i = \frac 1 Z \cdot \frac 1 { i \log i}$ where $Z$ is
a normalization factor. We requires the distribution produces a limited entropy
here.

# Proof

We try to approximate the optimal solution by iteratively selecting the optimal
code on partial distributions. 

Let $l_1^{(k)}, l_2^{(k)}, \cdots , l_k^{(k)}$ be the optimal solution for the
following integer optimization problem:
$$
\text{Minimize} \quad \sum_{i=1}^k p_il_i \\
\text{s.t.} \quad \sum_{i=1}^k 2^{-l_i}\leq1.
$$


If $\{l_t^{(k)}\}_ {k=1}^\infty$ is unbounded for some $t$, then 
$\sum_{i=1}^k p_il_i^{(k)}$ is also unbounded with respect to $k$. On the other
hand, set $l_t = \lceil\log \frac 1 {p_i}\rceil$ satisfying
$$
\sum_{i=1}^k 2^{-l_i}\leq \sum_{i=1}^k p_i < 1
$$
and we have
$$
\sum_{i=1}^k p_il_i < \sum_{i=1}^k p_i (\log \frac 1 {p_i} + 1)
$$
which is bounded with respect to $k$. Therefore, the minimal solution
$\sum_{i=1}^k p_il_i^{(k)}$ must also be bounded, which results in a
contradiction. Thus, $\{l_t^{(k)}\}_ {k=1}^\infty$ is bounded for any $t$.

Use $\mathscr{L_1^{(0)}, L_2^{(0)}, L_3^{(0)} \cdots}$ to denote all the series
$\{l_i^{(k)}\}_ {i=1}^k$ for $k=1,2,\cdots$.
There must be a number $l_1^\star$ that occurs infinite times at the starting
place amid these series due to boundness. Let's find all the series starting
with $l_1^\star$ among $\mathscr{L_1^{(0)}, L_2^{(0)}, L_3^{(0)}, \cdots}$ and
call them $\mathscr{L_1^{(1)}, L_2^{(1)}, L_3^{(1)}, \cdots}$. There must be a
number $l_2^\star$ that occurs infinite times at the second place amid these
series due to boundness. Let's find all the series whose second element is
$l_2^\star$ among $\mathscr{L_1^{(1)}, L_2^{(1)}, L_3^{(1)}, \cdots}$ and call
them $\mathscr{L_1^{(2)}, L_2^{(2)}, L_3^{(2)}, \cdots}$. Similarly, we would
derive a series $\mathscr{L^\star} :=\{l_i^\star\}_ {i=1}^\infty$. We will
prove $\mathscr{L^\star}$ is the optimal solution for the infinite source.

If it is not optimal, there must be a better series $\mathscr{\hat L} = \{\hat
l_i\}_ {i=1}^\infty$ such that
$$
\sum_{i=1}^\infty p_i\hat l_i < \sum_{i=1}^\infty p_il_i ^\star.
$$
There must be some $N$ that for any integer $n, m$ larger than $N$, we have
$$
\sum_{i=1}^m p_i\hat l_i < \sum_{i=1}^n p_il_i ^\star.
$$
On the other hand, according to how we define $l_i^\star$, there must be an
index $a$ such that the first $n$ elements of $\mathscr{L_a}$ are exactly
$l_1^\star, l_2^\star, \cdots, l_n^\star$. Note that 
$$
\sum_{i=1}^n p_il_i ^\star \leq \sum_{i=1}^a p_il_i ^\star \leq \sum_{i=1}^a p_i
\hat l_i. 
$$
Making $m = a$ produces a contradiction. Therefore $\mathscr{L^\star}$ is
optimal. $\blacksquare$



# For More Information
After proving the existence, I found [a
paper](https://ieeexplore.ieee.org/abstract/document/641571)
exactly on this topic. This paper also shows that the optimal code must satisfy
the Kraft inequality with equality. Read it if you are interested.
