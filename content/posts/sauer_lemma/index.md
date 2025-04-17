---
title: "Notes on Sauer's Lemma"
date: 2024-07-26T19:25:59+08:00
tags: ["AI", "theory", "statistics", "statistical learning", "combinatorics"]
categories: ["AI"]
draft: false
---

# Introduction

Every binary classifier is a function mapping its input, which is an element in
an enumerable dataset, to 0 or 1. Equivalently, we could regard the classifier
as a function $ f : \mathbb{N} \rightarrow \{ 0, 1 \} $. We have a set of
hypotheses $\mathcal{H}$ from which a function is chosen to maximize the
classification accuracy. It is perfect if $\mathcal{H}$ contains all possible
functions $ f : \mathbb{N} \rightarrow \{ 0, 1 \} $, which indicates a
universal approximator. However, when the expressiveness of our model is limited
by computational cost or the size of the magnitude of parameters, it remains a
problem to quantitatively measure the ability to approximate the ground truth.
For example, if $\mathcal{H}$ only consists of functions which produce 1 only
on one data point, namely,

$$ 
f_i (x) = 
\begin{cases}
1, & \text{if } x = i\\
0, & \text{otherwise}
\end{cases}, \quad i \in \mathbb{N},
$$

it is impossible to fit the data when the ground truths are all 1.

In statistical learning, we have two related metrics on this: the shattering
coefficient and VC (Vapnik–Chervonenkis) dimension.

**Shattering coefficient** $ S_{\mathcal{H}} (n) $ is defined as $ \sup_{k_1,
k_2, \ldots, k_n} | \{ (f  (k_1), f (k_2), \ldots, f (k_n)) : f \in \mathcal{H}
\} | $.

For example, in the following hypothesis, $ S_{\mathcal{H}} (1) = 2 $, $
S_{\mathcal{H}} (2) = 4 $ (for input 0,2), $ S_{\mathcal{H}} (3) = 5 $ (for
input 0,2,3).

| input | $f_1$ | $f_2$ | $f_3$ | $f_4$ | $f_5$ |
|-------|-------|-------|-------|-------|-------|
| 0     | 0     | 0     | 0     | 1     | 1     |
| 1     | 0     | 0     | 0     | 0     | 0     |
| 2     | 0     | 1     | 0     | 1     | 0     |
| 3     | 0     | 0     | 1     | 1     | 1     |
| others| 0     | 0     | 0     | 0     | 0     |

A hypothesis $\mathcal{H}$ shatters a set of inputs $ d_1, d_2, \ldots, d_t \in
\mathbb{N} $ if $ \# \{ (f (d_1), f (d_2), \ldots, f (d_t)) : f \in
\mathcal{H} \} = 2^t $. For example, the hypothesis above shatters $ \{ 0, 2
\} $ and $ \{ 0, 3 \} $ but does not shatter $ \{ 0, 1 \} $ or $ \{ 0, 1,
2 \} $.

For the sake of proving *Theorem*, we introduce the conditioned shattering
coefficient $ S_{\mathcal{H}, L} (n) = \sup_{k_1, k_2, \ldots, k_n \in L} | \{
(f  (k_1), f (k_2), \ldots, f (k_n)) : f \in \mathcal{H} \} | $ where $ L
\subseteq \mathbb{N} $.

**VC dimension** $ \mathcal{V}_{\mathcal{H}} $ is defined as $ \sup \{ | P | :
P \text{ is shattered by } \mathcal{H}, P \subseteq \mathbb{N} \} $.

Similarly, the conditioned VC dimension $ \mathcal{V}_{\mathcal{H}, L} $ is
defined as $ \sup \{ | P | : P \text{ is shattered by } \mathcal{H}, P
\subseteq L \} $.

A relationship between the shattering coefficient and the VC dimension is
unraveled by Sauer, Shelah, and Perles.

# Sauer-Shelah-Perles Lemma

## Theorem
$$ S_{\mathcal{H}} (n) \leqslant \sum_{i =
0}^{\mathcal{V}_{\mathcal{H}}} \binom{n}{i}. $$

## Proof
Without loss of generality, let $ | \{ (f  (1), f (2), \ldots, f (n))
 : f \in \mathcal{H} \} | = S_{\mathcal{H}} (n) $. And denote $\mathcal{R}$ as
a subset of $\mathcal{H}$ such that $ S_{\mathcal{H}} (n) = S_{\mathcal{R}} (n) $.

1. We first prove this theorem when the dataset only has $ n $ inputs, like $ 1,
   2, \ldots, n $ without loss of generality. In other words, we would like to
prove that

$$
S_ {\mathcal{H}, [n]} (n) \leqslant \sum_ {i = 0}^{\mathcal{V}_ {\mathcal{H},
[n]}} \binom{n}{i} 
$$

we would prove this special case by induction on $ n $. When $ n = 1 $, it is
obvious.

Now we would consider the induction from $ n $ to $ n + 1 $. We call two
functions $ f, g $ in the same type if $ f|_ {[n - 1]} = g|_ {[n - 1]} $. There
are at most two functions in the same type since they can only differ on the
output given the input $ n $. A representative set $ \mathcal{R}' $ is
constructed by choosing one element from every type. Every $ f |_ {[n - 1]} $ 
is distinct for every $ f \in \mathcal{R}' $. Therefore, $ |
\mathcal{R}' | = S_{\mathcal{R}', [n - 1]} (n - 1) $. Similarly, we get $ |
\mathcal{R} \backslash \mathcal{R}' | = S_{\mathcal{R} \backslash \mathcal{R}',
[n - 1]} (n - 1) $.

A simple estimation of the VC dimension is derived from
$\mathcal{V}_ {\mathcal{R}', [n - 1]} \leqslant \mathcal{V}_ {\mathcal{R}', [n]}
\leqslant \mathcal{V}_ {\mathcal{R}, [n]} $. The fact that any function in
$\mathcal{R} \backslash \mathcal{R}'$ has its representative in $\mathcal{R}'$
that only varies 0/1 on the input $ n $ indicates for any set $ K $ shattered by
$\mathcal{R} \backslash \mathcal{R}' $, $ K \bigcup \{ n \} $ can also be
shattered by $(\mathcal{R} \backslash \mathcal{R}') \bigcup \mathcal{R}'
=\mathcal{R} $, meaning $\mathcal{V}_ {\mathcal{R} \backslash \mathcal{R}', [n -
1]} \leqslant \mathcal{V}_ {\mathcal{R}, [n]} - 1 $.

  Combining all of them together obtains
$$
  \begin{align*}
    S_ {\mathcal{H}, [n]} (n) & =  S_ {\mathcal{R}, [n]} (n) = | \mathcal{R} |
    = | \mathcal{R}' | + | \mathcal{R} \backslash \mathcal{R}' |\\
    & =  S_ {\mathcal{R}', [n - 1]} (n - 1) + S_ {\mathcal{R} \backslash
    \mathcal{R}', [n - 1]} (n - 1)\\
    & \leqslant  \sum_ {i = 0}^{\mathcal{V}_ {\mathcal{R}', [n - 1]}} \binom{n
    - 1}{i} + \sum_ {i = 0}^{\mathcal{V}_ {\mathcal{R} \backslash \mathcal{R }',
    [n - 1]}} \binom{n - 1}{i}\\
    & \leqslant  \sum_ {i = 0}^{\mathcal{V}_ {\mathcal{R}, [n]}} \binom{n -
    1}{i} + \sum_ {i = 0}^{\mathcal{V}_ {\mathcal{R}, [n]} - 1} \binom{n -
    1}{i}\\
    & =  \sum_ {i = 0}^{\mathcal{V}_ {\mathcal{R}, [n]}} \binom{n - 1}{i} +
    \binom{n - 1}{i - 1}, \qquad ( \text{define} \binom{n - 1}{- 1} = 0)\\
    & =  \sum_ {i = 0}^{\mathcal{V}_ {\mathcal{H}, [n]}} \binom{n}{i} .
  \end{align*}
$$

  2. Then let's go back to the original theorem. Make $\mathcal{Q}= \{ f
  |_ {[n]} : f \in \mathcal{R}\}$ encompassing the functions
  induced from $\mathcal{R}$ on $[n] \{ 1, 2, \ldots, n \}$. Applying
  the limited conclusion we induced in the last part to $\mathcal{R}$ and
  $[n]$ shows that $S_ {\mathcal{H}} (n) = S_ {\mathcal{R}} (n) =
  S_ {\mathcal{Q}, [n]} (n) \leqslant \mathcal{V}_ {\mathcal{Q}, [n]}
  =\mathcal{V}_ {\mathcal{R}, [n]} \leqslant \mathcal{V}_ {\mathcal{R}}
  \leqslant \mathcal{V}_ {\mathcal{H}}$ which draws the conclusion.

**Comment**: Most proofs in textbooks on statistical learning ignore that both
$\mathcal{H}$ and $\mathbb{N}$ are infinite sets and the difference between
the *conditional* (VC dimension/shattering coefficient) and the *unconditional*
(VC dimension/shattering coefficient) on infinite sets.


# Appendix

An extension to this problem can be found 
[here](https://math.stackexchange.com/a/5055853/1131110).

For more proofs of the case of limited datapoints, check [this
article](https://cse.buffalo.edu/~hungngo/classes/2010/711/lectures/sauer.pdf)
where 3 proofs are delineated.

