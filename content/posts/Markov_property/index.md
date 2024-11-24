---
title: "Strictness of Markov Properties"
date: 2023-08-28T16:42:14+08:00
draft: false
tags: ["Markov", "theory"]
categories: ["Information theory"]
---

A stochastic process $\{X_i\}_{i=0}^\infty $ is $n$-Markov if 

$$P(X_{t+n}|X_{t+n-1}, X_{t+n-2}, \cdots , X_{t}) = P(X_{t+n}|X_{t+n-1})$$ 

for any $t \ge 0$.

We would prove that 
> An $n$-Markov stochastic process must be $m$-Markov while is not necessarily
> $l$-Markov where $l > n > m$

---


## N+1 to N

First, we prove **an (n+1)-Markov stochastic process must be n-Markov**.

*Proof*: Suppose $\{X_i\}_{i=0}^\infty$ is an $(n+1)$-Markov stochastic
process. We have

$$P(X_{t+n}|X_{t+n-1}, X_{t+n-2}, \cdots, X_t) = P(X_{t+n} | X_{t+n-1})$$ for
any $t \ge 0$, deriving

$$H(X_{t+n}|X_{t+n-1}, X_{t+n-2}, \cdots, X_t) = H(X_{t+n} | X_{t+n-1}).$$

Note that 

$$\begin{align*}
 & H(X_{t+n}|X_{t+n-1}, X_{t+n-2}, \cdots, X_{t+1}, X_t)  \\
\le & H(X_{t+n}|X_{t+n-1}, X_{t+n-2}, \cdots, X_{t+1}) \\
\le & \cdots \\
\le & H(X_{t+n} | X_{t+n-1}).
\end{align*}
$$

Therefore, these expressions have the same value which means

$$
\begin{align*}
  & I(X_{t+n};X{t}|X_{t+n-1}, X_{t+n-2}, \cdots, X_{t+1}) \\
= & H(X_{t+n}|X_{t+n-1}, X_{t+n-2}, \cdots, X_{t+1}) - H(X_{t+n}|X_{t+n-1}, X_{t+n-2}, \cdots, X_{t+1}, X_t) \\
= & 0.
\end{align*}
$$

Thus, $X_{t+n}$ and $X_t$ are independent given $X_{t+n-1}, \cdots , X_{t+1}$.
Using

$$
\begin{align*}
 & P(X_{t+n}|X_{t+n-1}, X_{t+n-2}, \cdots, X_{t+1}, X_{t}) \\
=& \frac{P(X_{t+n}, X_t |X_{t+n-1}, X_{t+n-2}, \cdots, X_{t+1})}{P(X_t
|X_{t+n-1}, X_{t+n-2}, \cdots, X_{t+1})} \\
=& P(X_{t+n}|X_{t+n-1}, X_{t+n-2}, \cdots, X_{t+1}),
\end{align*}
$$

iteratively, we could easily gain the conclusion.  
Q.E.D.

## N to N+1
Then we prove that **there exists an n-Markov process that is not (n+1)-Markov**.

The question is actually asking whether it is possible that knowing n preceding
states gains no more information than knowing the exact preciding state, but
knowing $(n+1)$ preciding states gains more information.

*Proof*: Consider a stationary stachastic process $\{X_i\}_{i=0}^\infty$ in
which $X_i$ is i.i.d. Bernoulli trial with $p = \frac12$ for $i=0,1,\cdots,n$
and

$$X_{t+n+1} = (X_{t+n} + \cdots + X_t)\, \text{mod}\, 2 $$

for $t \ge 0 $.

$P(X_{t+n+1}|X_{t+n}, X_{t+n-1}, \cdots, X_{t+1}, X_{t})$ is determined by its
$n+1$ preceding random variables. On the other hand, $P(X_{t+n+1}|X_{t+n},
X_{t+n-1}, \cdots, X_{t+1}) = 1/2$.

Q.E.D.
