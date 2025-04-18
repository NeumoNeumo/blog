---
title: "Existence of Points given Distances"
date: 2025-03-04T12:57:03+08:00
draft: false
---

Given the Euclidean distances between N points, what's the minimum
dimension where these N points exist?

More formally, given a positive integer $N \geq 2$ and positive numbers $a_{ij}$
for any $1\leq i, j\leq N$(and $a_{ij}=a_{ji}$), how to determine whether there
exist $N$ points in the K-dimensional Euclidean space such that the distance
between point $i$ and point $j$ is $a_{ij}$ for for any $1 \leq i, j\leq N$?

Yes. Adding new points iteratively to the construction solves this problem
easily because the distances between the newly added point and the points in our
current construction uniquely determine its position in the space. But here is a
more linear-algebraic solution.

**Solution**: Suppose in the K-dimensional points $x_1, x_2, \cdots x_n$
satisfy the requirements and $x_i = [x_{i1}, x_{i2},\cdots , x_{ik}]^T$.

Let $C = I - \frac 1 n 11^T$ be the centering matrix and $d_{ij} = \sum_{k=1}^K
(x_{ik} - x_{jk})^2$

Then we have

$$
\begin{align*}
(CDC)_ {ij} &= \sum_{1\leq u,v\leq N} C_{iu}D_{uv}C_{vj} \\
&=\sum_{1\leq u,v\leq N} C_{iu}C_{vj}\sum_{k=1}^K (x_{uk} - x_{vk})^2 \\
&=\sum_{1\leq u,v\leq N} C_{iu}C_{vj}\sum_{k=1}^K (x_{uk}^2 - 2x_{uk}x_{vk} + x_{vk}^2) \\
&=-2\sum_{1\leq u,v\leq N} C_{iu}C_{vj}\sum_{k=1}^K x_{uk}x_{vk} \\
&=-2\sum_{k=1}^K (\sum_{u=1}^N C_{iu} x_{uk})(\sum_{v=1}^N C_{jv} x_{vk})
\end{align*}
$$

Let $X = [x_1, x_2, \cdots, x_n]^T$. Then we get

$$CDC = -2CXX^TC.$$

So we have

1. $K\geq \text{rank}(X) \geq \text{rank}(CXX^TC) = \text{rank}(CDC)$
2. The eigenvalue of $CDC$ must be non-positive because the eigenvalue of RHS
   must be non-negative. 

Then we are going to prove that if the two conditions above are satisfied, we
can construct such N points in the K-dimensional space.

Suppose $CDC = \sum_{k=1}^K \lambda_k q_k q_k ^ T$ where $\lambda_k < 0$ are the
eigenvalues of $CDC$ and $q_k$ are the corresponding eigenvectors.

For any vector $v \in \text{ker}(C)$, $0=CDCv = \sum_{k=1}^K \lambda_k q_k q_k ^
T v$. Note that $q_k$ are linearly independent. We must have $\lambda_k q_k^T v
= 0$ which indicates $q_k$'s are in the column space of $CDC$. There exists
$u_k$ such that $Cu_k = \sqrt{-\frac {\lambda_k} {2}} q_k$ for $k=1,2,\cdots,K$.
Finally, let $X = [u_1, u_2, \cdots, u_k]. \quad \blacksquare$
