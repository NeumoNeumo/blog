---
title: "Intuition of Universal Approximation Theorem"
date: 2024-04-04T18:18:24-04:00
draft: false
tags: ["approximation", "theory"]
categories: ["AI"]
---

Universal approximation theorem states that an infinite width single layer
neural network is able to approximate an arbitrary continuous function
uniformly with a squashing function. It also have some stronger statement for
the approximation to Borel measurable function. But continuous function is
enough in our case. And we may intuitively expect that the space of all
continuous functions could approximate the space of Borel measurable functions
almost surely in the sense of probability. But we would not delve into the
details of it. For more information, check the original paper(Multilayer
Feedforward Networks are Universal Approximators).

# Notations

Given $g (\cdot) : \mathbb{R} \rightarrow \mathbb{R}$, use $\sum (g)$ to
denote the space of all the functions $\sum_{i = 1}^Q q_i g (A_i (\cdot))$
where $Q \in \mathbb{N}_ +, \\, q_i \in \mathbb{R} $ and $A_i (\cdot)$ are
affine transformations. The input dimension is $r$ and the output is a real
number. A squashing function is a non-decreasing function $f : \mathbb{R}
\rightarrow \mathbb{R}$ satisfying $\lim_{x \rightarrow - \infty} f (x) = 0$
and $\lim_{x \rightarrow \infty} f (x) = 1$. We are going to prove

> $\sum (g)$ is dense on the set of continuous functions from $\mathbb{R}^r$
> to $\mathbb{R}$, $C (\mathbb{R}^r, \mathbb{R})$, with uniform norm.

# Ideas

The most relevant theorem is Stone-Weierstrass Theorem:
> **(Stone-Weierstrass Theorem)** If $A$ is a complete unital
  sub-algebra of $C (K, \mathbb{R})$ that separates points on $K$ where $K$ is
  compact, then $A = C (K, \mathbb{R})$.

For simplicity, we denote the smallest Cauchy space that contains a set
$S$ as $\mathcal{C} (S)$. For sure, an all-zero affine transformation except
the bias term produces a constant function, which make $\sum (g)$ has the
multiplicative identity of $C (K, \mathbb{R})$. If $g$ is a squashing
function, it is also apparent that given any two points on $K$, there is
function in $\sum (g)$ that has distinct values on them. However, the
structure of algebra on a ring is multiplicative closed, which is not obvious
for $\sum (g)$. We first consider to complete $\sum (g)$ into a ring $\sum
\prod (g) := \left\\{ \sum_{i = 1}^Q q_i \prod_{j = 1}^{l_i} g (A_{i j}
(\cdot)) \right\\}$. Then $\sum \prod (g)$ is dense on $C (K, \mathbb{R})$. We
only need to prove every function $\sum \prod (g)$ can be approximated
uniformly by $\sum (g)$. However, we may add some restrictions or extensions
to $g$ to make those functions that we want to approximate have some good
properties. A good choice is trigonometric functions since the multiplication
of these functions is equivalent to sum of a set of trigonometric functions
which means $\sum \prod (\sin (\cdot)) = \sum (\sin (\cdot))$ and $\mathcal{C}
\left( \sum \prod (\sin (\cdot)) \right) = C (K, \mathbb{R})$ according to
Stone-Weierstrass Theorem. Therefore, all we need to do is proving
$\mathcal{C} \left( \sum (\sin (\cdot)) \right) =\mathcal{C} \left( \sum (g)
\right)$. We only need to prove a trigonometric function can be approximated
uniformly by $\sum (g)$ in one dimensional condition on any compact set which
is apparent because a squashing function can be seen like a Heaviside function
after applying extreme stretched affine transformation and any continuous
function can be approximated uniformly by step functions on a compact set.

# Useful Resources

1. The proof of the Stone-Weierstrass Theorem can be found
[here](https://wiki.math.ntnu.no/_media/ma8106/2020v/stoneweierstrass.pdf) (very
interesting)
2. [Brief notes on measure
   theory](https://www.math.ucdavis.edu/~hunter/measure_theory/measure_notes.pdf)

