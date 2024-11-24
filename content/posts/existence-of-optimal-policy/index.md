---
title: "Existence of Optimal Policy in Markov Decision Process"
date: 2022-09-12T19:00:44+08:00
draft: false
tags: ["existence theorem", "theory", "MDP"]
categories: ["RL", "AI"]
cover:
  image: "posts/existence-of-optimal-policy/img/Markov_Decision_Process.svg"
---

In this blog, we will prove the following theorem:
> *Optimal Policy Existence Theorem*:  
> For any Markov Decision Process,
> - There exists an optimal policy $\pi_\star $ that is better than or equal to all other policies, $ \pi_\star \geq \pi , \forall \pi$
> - All optimal policies achieve the optimal value function, $V_{\pi_\star}(s)=V_\star(s)$
> - All optimal policies achieve the optimal action-value function $Q_{\pi_\star}(s,a)=Q_\star(s,a)$

# Definition
To simplify the exposition, we first define some basic concepts.

**Rewards**: $R(s,a)$ is the random reward function when the agent takes action $a$ in the state $s$. And $r(s,a) = \mathbb E [R(s,a)]$ is the expected reward function which is only dependent on the corresponding state $s$ and action $a$.

**Next**: We attach a superscript *prime* to the upper-right of a symbol to denote its *successor*. For instance, $s^\prime$ is the next state of $s$ and $a^\prime$ is the next action following $a$.

**State-value Function**: $V_\pi(s) = \mathbb E_\pi \left[G_{t+1} | S_t = s\right]=\mathbb E_\pi \left[\sum_{i=1} \gamma^{i-1}r_{t+i}|S_t=s\right]$.

**Action-value Function**: $Q_\pi(s,a) = \mathbb E_\pi \left[G_{t+1} | S_t = s, A_t = a\right]=\mathbb E_\pi \left[\sum_{i=1} \gamma^{i-1}r_{t+i}|S_t=s, A_t = a\right]$.

**Optimal State-value Function**: $V_\star (s) = \max_\pi \left\{ V_\pi(s) \right\}$.

**Optimal Action-value Function**: $Q_\star (s, a) = \max_\pi \left\{ Q_\pi(s,a) \right\}$.

**Partial Order Relation**: Given two policy $\pi_1$ and $\pi_2$, we have $\pi_1 > \pi_2$, if and only if for all states $s$, $V_{\pi_1} > V_{\pi_2}$ holds. (Other partial order symbols like $<$ and $\leq$ follow similar definitions)

**Optimal Policy**: A policy $\pi_\star$ is optimal if and only if $\pi_\star \geq \pi$ for all states $\pi$.

# Prerequisite
## Bellman Optimality Equation
We are going to probe into the existence of optimal policy. So before delving into the formal proof of this theorem, we explore some useful properties of optimal policy in advance.

> *Proposition I*: $$
\pi_\star(a|s) = 0,
$$ if $Q_{\pi_\star}(s,a) < \max_{\tilde{a}} Q_{\pi_\star}(s,\tilde{a})$.

**Proof** of *Proposition I*:

If the statement does not hold for an optimal policy $\pi_\star$, we construct a new policy $$\hat\pi(a|s) = \begin{cases}
    1, & a = \arg\max_{\tilde{a}} Q_{\pi_\star}(s,\tilde{a}) \\
    0, & \text{otherwise}
\end{cases}$$
(If there are multiple maximum points in $\arg\max$, only choose arbitrary one.)

Then we have
$$\begin{align*}
V_{\pi_\star}(s) &= \sum_a \hat \pi (a | s) \left(r(s,a) + \gamma \sum_{s^\prime} p(s^\prime|s,a) V_{\pi_\star}(s^\prime)\right) \\
&\leq \sum_a \pi _ \star (a|s) \left( r(s,a) + \gamma \sum_{s^\prime} p(s^\prime | s,a) V_{\pi_\star}(s^\prime) \right).
\end{align*}
$$
In another word, we conclude that
$$
V_{\pi_\star}(s) \leq \mathbb E_{a \sim \hat\pi} [R(s,a) + \gamma V_{\pi_\star}(s^\prime)] \tag{1},
$$ where $s^\prime$ represents the next state.
Employing this formula iteratively derives a series of inequalities
$$\begin{align*}
V_{\pi_\star}(s) &\leq \mathbb E_{a \sim \hat\pi} [R(s,a) + \gamma V_{\pi_\star}(s^\prime)] \\
&\leq \mathbb E_{a \sim \hat\pi} [R(s,a) + \gamma \mathbb E_{a^\prime \sim \hat \pi}[R(s^\prime, a^\prime)] + \gamma V_{\pi_\star}(s^{\prime\prime}) ] \\
&= \mathbb E_{\hat \pi} [R(s,a) + \gamma R(s^\prime, a^\prime) + \gamma^2 V_{\pi_\star}(s^{\prime\prime})] \\
&\leq \mathbb E_{\hat \pi} [R(s,a) + \gamma R(s^\prime, a^\prime) + \gamma^2 R(s^{\prime\prime}, a^{\prime\prime}) + \cdots] \\
&= V_{\hat\pi}(s).
\end{align*}
$$
We call the states $s$ as suboptimal states if there exits an action $a$ s.t. $\pi_\star(a|s)\neq 0 $ and $ Q_{\pi_\star}(s,\tilde{a})<\max_{\tilde{a}}\{Q_{\pi_\star}(s,\tilde{a})\}$
In this process, the partial order in (1) cannot always be equal signs if $s^\prime$ is a suboptimal state. Therefore, $V_{\pi_\star} \leq V_{\hat\pi}$ and for suboptimal states $s$, we conclude that $V_{\pi_\star}(s) < V_{\hat\pi}(s)$ which means that the policy $\pi_\star$ is not an optimal policy, leading to a contradiction.

Q.E.D.

> *Corollary II (Bellman Optimality Equation)*: $$ V_{\pi_\star}=\max_a \{ r(s,a) + \gamma \sum_{s^\prime} p(s^\prime|s,a) V_{\pi_\star}(s^ \prime ) \}.$$

**Proof** of *Corollary II*:

According to *Proposition I*, we acquire that $V_{\pi_\star} = \max_a \{Q(s,a)\}$. Expanding $Q(s,a)$ directly derive the corollary.

**Remark**: *Corollary II* proves a necessary condition as an optimal policy.

## Unique Solution
In this section, we will prove that there is a unique solution of the *Bellman Optimality Equation*.

> *Lemma I*:  
> Given $\mathbf a, \mathbf b \in \mathbb R^n$, we have
> $ |\max \{\mathbf a\} - \max \{\mathbf b\}| \leq \max |\mathbf a-\mathbf b|. $

**Proof** of *Lemma I*:
Let $\mathbf a = (a_1, a_2, \cdots, a_n)$ and $\mathbf b = (b_1, b_2, \cdots , b_n)$. We set $a_u = \max _i \{ a_i\}$ and $b_v = \max _i \{ b_i \}$ and without loss of generality, $a_u \geq b_v$.
$$\begin{align*}
|\max \{\mathbf a\} - \max \{\mathbf b\}| &= a_u - b_v \\
&= (a_u - b_u) + (b_u - b_v) \\
&\leq a_u - b_u \leq \max\{ \mathbf a - \mathbf b \}
\end{align*}
$$
Q.E.D.


> *Lemma II*:  
> The *Bellman Optimality Equation* has a unique solution $\hat V_\star$.

**Proof** of *Lemma II*:

We use $\mathcal U$ to denote the set of all function $V\colon S \rightarrow \mathbb R$ where $S$ denotes all the states.

A transformation 
$$T\colon \mathcal{U} \rightarrow \mathcal{U}, V \mapsto \max_a \{r(s,a) + \gamma \sum_{s^\prime} p(s^\prime | s, a) V(s^\prime) \} $$ 
is utilized to iteratively approximate the optimal policy.

We would prove that the transformation is a contraction mapping in the space $\mathcal{U}$ with $\mathcal{l}^\infty$-norm, namely $\max_s \{V(s)\}$. Then the lemma can be derived according to *Banach fixed-point theorem*.

For $V_1, V_2 \in \mathcal{U}$, using *Lemma I*, we obtain
$$
\begin{align*}
\lVert T(V_1) - T(V_2) \rVert _\infty &= \max_s \; \biggr | \max_a\{ r(s,a)+\gamma \sum _{s^\prime} p(s^\prime | s,a) V_1(s^\prime) \} \\ 
&\quad\quad\quad -\max_a \{ r(s,a) + \gamma \sum _{s^\prime} p(s^\prime | s,a) V_2 (s^\prime)  \} \biggr | \\
&\leq \max _s \biggr \{ \max _a \; \biggr | r(s,a) + \gamma \sum _{s^\prime} p(s^\prime | s,a) V_1 (s^\prime)  \}  \\
&\quad\quad\quad - r(s,a) - \gamma \sum _{s^\prime} p(s^\prime | s,a) V_1 (s^\prime)  \} \biggr | \biggr \} \\
&= \gamma \max _s \biggr \{ \max _a \biggr | \sum _{s^\prime} p(s^\prime | s,a) (V_1(s^\prime) - V_2(s^\prime)) \biggr | \biggr \} \\
&\leq \gamma \max _s \left \{ \max _a \biggr | \sum _{s^\prime} p(s^\prime | s,a) V _{\max} \biggr | \right \} \\
& = \gamma \max _s \left \{ \max _a | V _{\max} | \right \} \\
& = \gamma V _{\max}
\end{align*}
$$

where $V_{\max} = \lVert V_1 - V_2 \rVert _\infty$. Because $\gamma$ is a positive number that is less than 1, we conclude that $T$ is a contradiction mapping, thus proving this lemma.

Q.E.D.

## Sufficient Condition
We have proved that all optimal policies must satisfy *Bellman Optimality Equation* and that *Bellman Optimality Equation* must have a unique solution $\hat V_\star$. In the last step, we will unveil that the policy correspond to $\hat V_\star$ is actually an optimal policy.

The transformation $T$ we used in the proof of *Lemma II* is quite important in Markov Decision Process. So let us re-emphasize the definition of $T$ and bring out a beneficial lemma from it.

$$T\colon \mathcal{U} \rightarrow \mathcal{U}, V \mapsto \max_a \{r(s,a) + \gamma \sum_{s^\prime} p(s^\prime | s, a) V(s^\prime) \} $$ 
where $\mathcal U$ denotes the set of all function $V\colon S \rightarrow \mathbb R$ and $S$ denotes all the states.

> *Lemma III*: If $V \in \mathcal U$ is a state-value function, then $T(V) \geq V.$

**Remark**: This lemma is just rewriting what we did in *Proposition I*. Do you remember how we prove this lemma there? In addition, please check the **Definition** section if you forget what the $\geq$ symbol means here.

> *Lemma IV*:  
> If the state-value function $V$ of a policy $\pi$ satisfies the *Bellman Optimality Equation*, then $V$ is an optimal state-value function.

**Proof** of *Lemma IV*:

According to *Lemma II*, we know that $V$ is actually the unique solution $\hat V_\star$. If there exists a state-value function $ \tilde V$ s.t. $\tilde V(\tilde s) > V(\tilde s)$ at some state $\tilde s$. Using the transformation $T$, we get $\hat V = \lim _{n \rightarrow \infty} T^{n}(\tilde V) $. According to *Lemma II*, $\hat V$ is exactly $\hat V _\star$ as well. Through the repeated application of *Lemma III*, an inequality can be obtained
$$
\begin{align*}
    \hat V _\star(\tilde s) = \hat V(\tilde s) &= (\lim _{n \rightarrow \infty} T^n(\tilde V))(\tilde s) \\
    &\geq \tilde V(\tilde s) > V (\tilde s) = \hat V _\star (\tilde s),
\end{align*}
$$
which leads to a contradiction.  
Therefore, for all $\tilde V$, the inequality $V \geq \tilde V$ always holds.  
Q.E.D.

**Remark**: *Lemma IV* togetehr with the necessary condition of an optimal state-value function we stated in *Corollary* implies the equivalence between *Bellman Optimality Equation* and optimality of a state-value function.

# Existence Theorem
In this section, we will prove our target theorem in this blog.

> *Optimal Policy Existence Theorem*:  
> For any Markov Decision Process,
> - There exists an optimal policy $\pi_\star $ that is better than or equal to all other policies, $ \pi_\star \geq \pi , \forall \pi$
> - All optimal policies achieve the optimal value function, $V_{\pi_\star}(s)=V_\star(s)$
> - All optimal policies achieve the optimal action-value function $Q_{\pi_\star}(s,a)=Q_\star(s,a)$

**Proof** for *Optimal Policy Existence Theorem*:

We first prove that the deterministic greedy policy 
$$
\pi \colon S \rightarrow A, s \mapsto \arg\max _ a \{r(s,a) + \gamma \sum _ {s^\prime} p(s^\prime|s,a) V_\star(s^\prime)  \}
$$ exactly produces $V_\pi$ same as $V_\star$.

According to *Bellman Optimality Equation*, we have
$$\begin{align*}
V _ \star(s) &= \max_a \{ r(s,a) + \gamma \sum _ {s^\prime} P(s^\prime|s,a) V _ \star(s ^ \prime)  \} \\
&= \mathbb E _{a \sim \pi} [ r(s,a) + \gamma \sum _ {s^\prime} P(s^\prime|s,a) V _ \star(s ^ \prime) ].
\end{align*}
$$
Expand $V _\star$ in the expectation expression and we further derive
$$
\begin{align*}
    V _\star(s) &= \mathbb{E} _\pi [r(s,a) + \gamma r(s^\prime, a^\prime) + \gamma^2 r(s^{\prime\prime}, a^{\prime\prime}) + \cdots] \\
    &= V _\pi(s).
\end{align*}
$$

Therefore, $V _\pi$ satisfies *Bellman Optimality Equation*, making $V _\pi$ the optimal state-value function and $\pi$ the optimal policy using *Lemma IV*. The first statement has been proved.

An optimal policy has an optimal state-value function by definition. So the second statement is achieved.

For any policy $\tilde \pi$
$$
\begin{align*}
    Q_\pi(s,a) &= r(s,a) + \sum _a P(s^\prime | s, a) V _\star(s^\prime) \\
    &\geq r(s,a) + \sum _a P(s^\prime | s, a) V _{\tilde \pi}(s^\prime) \\
    &= Q _{\tilde \pi}(s,a),
\end{align*}
$$
meaning that $Q _\pi$ is an optimal action-value function. So the last statement is proved.

Q.E.D.

# Reference
This post mainly refers to [a post](https://towardsdatascience.com/why-does-the-optimal-policy-exist-29f30fd51f8c#:~:text=In%20a%20finite%20Markov%20Decision,the%20value%20of%20state%20s') by Alireza Modirshanechi. In that post, however, Modirshanechi did not consider the sufficiency of the iterated limit result. This post proffers a detailed explanation as a supplement.
