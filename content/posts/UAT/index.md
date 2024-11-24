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
where $Q \in \mathbb{N}_ +, \, q_i \in \mathbb{R} $ and $A_i (\cdot)$ are
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
\prod (g) := \left\{ \sum_{i = 1}^Q q_i \prod_{j = 1}^{l_i} g (A_{i j}
(\cdot)) \right\}$. Then $\sum \prod (g)$ is dense on $C (K, \mathbb{R})$. We
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

## Quick Recap

1. An **algebraic structure** $(X, \oplus)$ consists of a set $X$ and
an internal binary operator "$\oplus$" which means $x \oplus y \in X$ for
any $x, y \in X$.

Conventionally, we may also omit the operator and simply call the algebraic
structure $X$ if there's no ambiguity.

2. A **semigroup** is an algebraic structure $(X, \oplus)$ that has an
associative operator, which means $(x \oplus y) \oplus z = x \oplus (y
\oplus z)$ for any $x, y, z \in X$.

3. A **monoid** is a semigroup $(X, \oplus)$ and there is an identity
element $e \in X$ such that $e \oplus x = x \oplus e = x$ for any $x \in X$.

4. A **group** is a monoid $(X, \oplus)$ and \ for any $x \in X$ there
exists an element $y \in X$ such that $x \oplus y = y \oplus x = e$ where
$e$ is the identity element the monoid.

If the operator in a group $(X, \oplus)$ is commutative ($x \oplus y = y
\oplus x$ for any $x, y \in X$), then the group is an **abelian
group**.

5. A **ring** is a triple $(X, +, \ast)$ such that   
  i. $(X, +)$ is an abelian group;   
  ii. $(X, \ast)$ is a monoid;   
  iii. Distributivity is hold: $x \ast (y + z) = x \ast y + x \ast z$ and $(x +
  y) \ast z = x \ast z + y \ast z$ for any $x, y, z \in X$.

Conventionally, $0$ is used to denote the additive identity and $1$ is used to
denote the multiplicative identity. A ring is commutative if the
multiplicative operator of a ring is commutative. We may omit $\ast$ if
there's no ambiguity like $a \ast b = a b$.

6. A **field** is a ring $(X, +, \ast)$ that has multiplicative
inverses for all elements except $0$. On the other words, for every $x \in
X$ and $x \neq 0$, there exists an element $y \in X$ such that $x \ast y = y
\ast x = 1$.

7. An **algebra** over a field $K$ is a vector space A with a bilinear
operator $\cdot$ mapping from $A \times A$ to $A$ such that  
  i. $(\lambda x) \cdot y = x \cdot (\lambda y) = \lambda (x \cdot y)$ for any
$\lambda \in K, x, y \in A$;  
  ii. $(x + y) \cdot z = x \cdot z + y \cdot z$ and $x \cdot (y + z) = x \cdot
y + x \cdot z$ for any $x, y, z \in A$.  

A **unital algebra** contains a multiplicative identity. A
sub-algebra of $A$ that contains the multiplicative identity of $A$ is called
a **unital sub-algebra**. It is possible that the algebra and its
sub-algebra have different multiplicative identities. In such cases, the
sub-algebra is unital but is not called unital sub-algebra.

8. The **center** $Z (R)$ of a ring $R = (X, +, \ast)$ is a set
  consisting all $c \in X$ such that $c x = x c$ for any $x \in X$.

The center of a ring is a subring.

9. A **ring homomorphism** is a structure-preserving function $f : R
  \rightarrow S$ where R and S are both rings, which means $f (x + y) = f (x) f
  (y)$ and $f (x y) = f (x) f (y)$ for any $x \in R$ and $y \in S$.

Note that the operators $+$ and $\ast$ above on the two sides of the equation
are defined on different rings. We write them in the same symbol if there's no
ambiguity.

10. An **associative algebra** over a commutative ring $K$ is tuple
$(A, f)$ where $A$ is a ring and $f$ is a ring homomorphism from K into $Z
(A)$ that is the center of $A$.

11. We use $\mathcal{P} (X)$ to denote the power set of $X$ which includes all
subsets of $X$.

12. A **topological space** $(X, C)$ has a set $X$ and a collection of
open sets $C \subseteq \mathcal{P} (X)$ satisfying the following property:   
  i. $\varnothing, X \in C$;   
  ii. For any collection $D \subseteq C$, the union of all sets in $D$ is also
  open, or $\bigcup D \in C$;  
  iii. For any finite collection $D \subseteq C$, the intersection of all sets
  in D is also open, or $\bigcap D \in C$. 

Finity in the third condition is vital since $\bigcap \{ (- 1 / n, 1 / n) : n
\in \mathcal{N}_ + \} = \{ 0 \}$ which is not regarded as an open set in common
cases when considering a topological space defined on real numbers $R$ and C
being the collection of open intervals.

13. A **metric(distance function)** on a set $X$ is a function $d : X
    \rightarrow X$ that satisfies the following properties  
  i. Non-negativity: $d (x, y) \geqslant 0$ for any $x, y \in X$  
  ii. Positive definiteness: $d (x, y) = 0$ if and only if $x = y$;  
  iii. Symmetry: $d (x, y) = d (y, x)$ for any $x, y \in X$;  
  iv. Triangle inequality: $d (x, y) + d (y, z) \geqslant d (x, z)$ for any $x,
  y \in X$.

The set X together with its metric constitutes a **metric space**.

A metric space is **complete** if every limit of a Cauchy sequence in
it is still in it.

14. A **normed vector space** is a vector space $V$ over $K$(like
  $\mathbb{R}$ or $\mathbb{C}$) with a norm $\| \cdot \|$ defined satisfying
  the following axioms:  
  i. Non-negativity: $\| x \| \geqslant 0$ for any $x \in$V;  
  ii. Positive definiteness: $\| x \| = 0$ if and only if $x$ is the zero
  vector;  
  iii. Absolute homogeneity: $\| \lambda x \| = \lambda \| x \|$ for any
  $\lambda \in K, \, x \in V$.  
  iv. Triangle inequality: $\| x \| + \| y \| \geqslant \| x + y \|$ for any
  $x, y \in X$.  

A normed vector space must be a metric space sinply by using the metric
function $\| x - y \|$. A complete normed vector space is also called
**Banach space**. If an associative algebra over real or complex
numbers is a Banach space, it is called **Banach algebra**.

15. The **uniform closure** of a set of functions consists all the
  functions that can be uniformly approximated by a sequence of functions in
  this set.

