---
title: "Low-Rank Emergence (1)"
date: 2026-07-18T14:15:42+08:00
draft: false
---

This post begins a series of extensions to our previous post, [The Neural
Matthew Effect: Low Effective Degrees of Freedom in
Training](/blog/posts/matthew). We want to understand, at least partially, how
a full-rank matrix can turn into an effectively low-rank one during training.

Here, we use *low rank* in a broad sense: only a small fraction of the neural
connections play a decisive role in the function represented by the network.
Several quantities can describe this phenomenon, including effective rank and
stable rank; see the [previous post](/blog/posts/matthew) for their definitions.

Our first attempt starts with a deep linear network

$$
W = W_L W_{L-1}\cdots W_1.
$$

Even when this product can represent any matrix, could optimizing the factors
instead of the product itself create an implicit bias? We will begin with the
simplest tied two-layer factorization, $X=UU^\top$.

## Notation and setup

For vectors, $\odot$ denotes the [Hadamard
product](https://en.wikipedia.org/wiki/Hadamard_product_%28matrices%29). Thus,
$u\odot u$ is the vector whose $i$-th entry is $u_i^2$. We will always use
parentheses when Hadamard and matrix products appear together.

For matrices, let $\mathbb{S}^n$ be the space of real symmetric $n\times n$
matrices, and define a linear measurement operator

$$
\mathcal A:\mathbb{S}^n\to\mathbb{R}^m,
\qquad
\mathcal A(X) = \begin{bmatrix}
\langle A_1,X\rangle_F & \cdots & \langle A_m,X\rangle_F
\end{bmatrix}^{\top}.
$$

Its adjoint is

$$
\mathcal A^*(\lambda)=\sum_{j=1}^m \lambda_j A_j.
$$

This formula follows from the definition of an adjoint. We want

$$
\langle \mathcal A(X),\lambda\rangle_2
=\langle X,\mathcal A^*(\lambda)\rangle_F
$$

for every $X$ and $\lambda$. Since the left-hand side is
$\sum_j\lambda_j\langle A_j,X\rangle_F$, collecting the matrices $A_j$ gives
exactly $\mathcal A^*(\lambda)=\sum_j\lambda_jA_j$.

All the dynamics below are gradient flow, $\dot\theta=-\nabla_\theta f$.
Gradient descent with a small step size is its discrete analogue.

## Main

### A linear warm-up

Consider ordinary least squares,

$$
\min_x \frac12\lVert Ax-y\rVert_2^2.
$$

If $Ax=y$ is consistent, Landweber iteration (gradient descent initialized at
$x_0=0$) converges to the solution with minimum $\ell^2$ norm. A brief proof is
given in [Appendix A](#appendix-a-why-landweber-iteration-selects-the-minimum-norm-solution).

This is already an implicit bias: the loss only asks for *a* solution, but the
optimization path selects a particular one. What happens if we change only the
parameterization?

### The diagonal model: squaring the parameters

Consider

$$
\min_u f(u),
\qquad
f(u)=\frac12\lVert A(u\odot u)-y\rVert_2^2.
$$

Write

$$
x=u\odot u\geq 0,
\qquad
r=y-Ax,
$$

and let $a_i$ be the $i$-th column of $A$. Gradient flow in $u$ is

$$
\dot u=2\bigl(A^\top r\bigr)\odot u.
$$

The extra factor $u$ changes the dynamics completely. Since
$\dot x=2u\odot\dot u$, each coordinate of $x$ obeys

$$
\dot x_i=4x_i a_i^\top r.
$$

Suppose $u(0)=\sqrt{\varepsilon}\,\mathbf 1$, so that
$x(0)=\varepsilon\mathbf 1$. At the beginning, $x$ is tiny and $r\approx y$,
so

$$
\dot u_i\approx 2(a_i^\top y)u_i.
$$

Thus the coordinates initially grow at different exponential rates. A
coordinate with a large correlation $a_i^\top y$ is likely to emerge first
from the microscopic scale. Once it becomes macroscopic, it changes the
residual $r$; the growth rates are then rearranged, and another coordinate may
start to emerge. This is the first hint of a sparse, stage-by-stage process.

### A resemblance to OMP

This picture reminds us of Orthogonal Matching Pursuit (OMP) for $Ax=y$:

1. Start with residual $r_0=y$, support $T=\varnothing$, and $t=0$.
2. Add to $T$ the column $a_i$ with the largest correlation with $r_t$.
3. Project $y$ onto the span of the selected columns, and call the new
   residual $r_{t+1}$.
4. Increase $t$ and repeat until the residual is sufficiently small.

The resemblance is only qualitative. OMP makes a discrete, irreversible
choice, whereas every coordinate in the gradient-flow dynamics keeps evolving.
OMP also need not return a minimum-$\ell^1$ solution.

For example, let

$$
A=
\begin{bmatrix}
1 & \frac35 & 0\\
0 & \frac45 & 1
\end{bmatrix},
\qquad
y=
\begin{bmatrix}
1\\[2pt]
\frac1{10}
\end{bmatrix}.
$$

OMP first selects the first column and then the third, giving

$$
x_{\mathrm{OMP}}=
\begin{bmatrix}1&0&\frac1{10}\end{bmatrix}^{\top},
\qquad
\lVert x_{\mathrm{OMP}}\rVert_1=\frac{11}{10}.
$$

But

$$
\tilde x=
\begin{bmatrix}\frac{37}{40}&\frac18&0\end{bmatrix}^{\top}
$$

also satisfies $A\tilde x=y$, and
$\lVert\tilde x\rVert_1=\frac{21}{20}<\frac{11}{10}$.

### Why an $\ell^1$ solution appears

Because $x=u\odot u$ is nonnegative, the relevant convex problem is

$$
\begin{aligned}
\min_{x\geq 0}\quad &\mathbf 1^\top x\\
\text{subject to}\quad &Ax=y.
\end{aligned}
\tag{P}
$$

On the nonnegative orthant, $\mathbf 1^\top x=\lVert x\rVert_1$. The
Lagrangian is

$$
L(x,\lambda)
=\mathbf 1^\top x-\lambda^\top(Ax-y)
=(\mathbf 1-A^\top\lambda)^\top x+y^\top\lambda.
$$

Taking the infimum over $x\geq0$ gives the dual problem

$$
\begin{aligned}
\max_\lambda\quad &y^\top\lambda\\
\text{subject to}\quad &A^\top\lambda\leq\mathbf 1.
\end{aligned}
\tag{D}
$$

Therefore, it is enough to find a dual-feasible $\lambda$ such that

$$
a_i^\top\lambda=1
\quad\text{whenever}\quad \bar x_i>0.
\tag{1}
$$

Indeed, these conditions would give

$$
\mathbf 1^\top\bar x
=\sum_i \bar x_i a_i^\top\lambda
=\lambda^\top A\bar x
=y^\top\lambda,
$$

so the primal and dual objectives agree.

Now return to the dynamics. Dividing $\dot x_i$ by $x_i$ and integrating,

$$
\log\frac{x_i(t)}{\varepsilon}
=a_i^\top q(t),
\qquad
q(t)=4\int_0^t r(s)\,\mathrm ds.
\tag{2}
$$

This looks surprisingly close to the dual conditions. Define

$$
\lambda_\varepsilon(t)
=\frac{q(t)}{-\log\varepsilon}.
$$

Equation (2) becomes

$$
x_i(t)=\varepsilon^{\,1-a_i^\top\lambda_\varepsilon(t)}.
\tag{3}
$$

Here is the core of the limiting argument. Assume that, for each
$\varepsilon$, the flow reaches a zero-loss limit $x_\varepsilon(\infty)$,
and that these solutions remain bounded and converge to $\bar x$ as
$\varepsilon\downarrow0$. Also take a convergent subsequence of the
corresponding $\lambda_\varepsilon(\infty)$ and call its limit $\lambda$.
Along this subsequence:

- boundedness in (3) forces $a_i^\top\lambda\leq1$; otherwise $x_i$ would
  blow up as $\varepsilon\downarrow0$;
- if $\bar x_i>0$, the exponent in (3) must approach zero, so
  $a_i^\top\lambda=1$.

These are exactly dual feasibility and (1). Consequently, under these limit
assumptions, infinitesimal initialization selects a minimum-$\ell^1$ solution
of (P). The calculation is not quite OMP, but it explains the same
coordinate-by-coordinate flavor more cleanly: the logarithms of the parameters
are building a dual certificate.

### From vectors to positive-semidefinite matrices

Now consider the tied matrix factorization

$$
\min_U \frac12\lVert\mathcal A(UU^\top)-y\rVert_2^2,
\qquad
X=UU^\top\succeq0.
$$

Let $r=y-\mathcal A(X)$ and assume that every measurement matrix $A_j$ is
symmetric. The gradient-flow equations are

$$
\dot U=2\mathcal A^*(r)U
$$

and therefore

$$
\dot X
=\dot U U^\top+U\dot U^\top
=2\mathcal A^*(r)X+2X\mathcal A^*(r).
\tag{4}
$$

The matrix analogue of (P) is

$$
\begin{aligned}
\min_{X\succeq0}\quad &\operatorname{Tr}(X)\\
\text{subject to}\quad &\mathcal A(X)=y.
\end{aligned}
\tag{MP}
$$

Since $X\succeq0$, its trace is both its nuclear norm and its Schatten
$1$-norm. Its Lagrangian has the same shape as before:

$$
L(X,\lambda)
=\left\langle I-\mathcal A^*(\lambda),X\right\rangle_F
+y^\top\lambda.
$$

Taking the infimum over $X\succeq0$ gives the dual problem

$$
\begin{aligned}
\max_\lambda\quad &y^\top\lambda\\
\text{subject to}\quad &\mathcal A^*(\lambda)\preceq I.
\end{aligned}
\tag{MD}
$$

Therefore, the remaining optimality conditions ask for a vector $\lambda$ such
that

$$
\mathcal A^*(\lambda)\preceq I,
\qquad
\left\langle I-\mathcal A^*(\lambda),\bar X\right\rangle_F=0.
\tag{5}
$$

To make the dynamics as transparent as in the vector case, we now need one
extra assumption: the measurement matrices commute pairwise,

$$
A_iA_j=A_jA_i\qquad\text{for all }i,j.
$$

Because they are symmetric, they can then be diagonalized in the same basis,
and the matrices
$\mathcal A^*(r(t))$ commute across time. Starting from
$U(0)=\sqrt\varepsilon I$ for a full-width factor, hence
$X(0)=\varepsilon I$, equation (4) integrates to

$$
X_\varepsilon(t)
=\varepsilon\exp\left(
4\mathcal A^*\!\left(\int_0^t r(s)\,\mathrm ds\right)
\right).
\tag{6}
$$

Define, in parallel with the vector case,

$$
\lambda_\varepsilon(t)
=\frac{4\int_0^t r(s)\,\mathrm ds}{-\log\varepsilon}.
$$

Then (6) can be written as

$$
X_\varepsilon(t)
=\exp\left(
\log\varepsilon\,[I-\mathcal A^*(\lambda_\varepsilon(t))]
\right).
\tag{7}
$$

Equation (7) is the matrix version of (3). Along a subsequence where
$\lambda_\varepsilon(\infty)$ converges to $\lambda$, all these matrices share
an eigenbasis. Boundedness as $\varepsilon\downarrow0$ forces every eigenvalue
of $I-\mathcal A^*(\lambda)$ to be nonnegative. Any direction in which
$\bar X$ has positive mass must have eigenvalue zero. These are precisely the
two conditions in (5).

Thus, if the zero-loss limit

$$
\bar X=\lim_{\varepsilon\downarrow0}X_\varepsilon(\infty)
$$

exists (together with the dual limit point used above), then in the commuting
case it solves (MP): gradient flow on the factorization selects a
minimum-nuclear-norm positive-semidefinite solution. Without commutativity, the
simple exponential formula (6) no longer follows, so this argument does not
settle the general case.

## Summary

The three optimization paths now form a suggestive progression:

- optimizing $x$ directly uses additive dynamics and selects a minimum
  $\ell^2$-norm solution;
- optimizing $x=u\odot u$ uses multiplicative coordinate dynamics and, from
  infinitesimal initialization, selects a minimum $\ell^1$-norm nonnegative
  solution;
- optimizing $X=UU^\top$ produces the matrix version of those multiplicative
  dynamics and, for commuting measurements, selects a minimum nuclear-norm
  solution.

This does not yet explain low-rank emergence in general deep networks. But it
does show a concrete mechanism by which a seemingly harmless factorization
changes the geometry of the optimization path---and changes which interpolating
solution is preferred.

## Appendix A: Why Landweber iteration selects the minimum-norm solution

Landweber iteration for least squares is

$$
x_{k+1}=x_k-\eta A^\top(Ax_k-y),
\qquad
0<\eta<\frac{2}{\lVert A\rVert_2^2}.
$$

Assume $Ax=y$ is consistent and $x_0=0$. Every update lies in
$\operatorname{range}(A^\top)$, so every iterate does too. On this subspace,
the eigenvalues of $I-\eta A^\top A$ have absolute value less than one;
therefore the iterates converge to the unique solution
$x^\dagger\in\operatorname{range}(A^\top)$.

Every other solution has the form $x^\dagger+z$ with
$z\in\ker(A)$. Since
$\operatorname{range}(A^\top)=\ker(A)^\perp$,

$$
\lVert x^\dagger+z\rVert_2^2
=\lVert x^\dagger\rVert_2^2+\lVert z\rVert_2^2
\geq\lVert x^\dagger\rVert_2^2.
$$

Hence $x^\dagger=A^\dagger y$ is the minimum-$\ell^2$-norm solution. The
zero initialization matters: a nonzero component in $\ker(A)$ is never changed
by the iteration.

## Reference

Suriya Gunasekar, Blake Woodworth, Srinadh Bhojanapalli, Behnam Neyshabur, and
Nathan Srebro. [Implicit Regularization in Matrix
Factorization](https://arxiv.org/abs/1705.09280), 2017.
