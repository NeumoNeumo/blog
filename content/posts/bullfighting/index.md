---
title: "Puzzle: Can a Matador Always Dodge a Bull's Charge?"
date: 2025-12-05T17:08:01+08:00
tags: ["game", "math", "puzzle"]
categories: ["Fun"]
draft: false
---

# Puzzle

Play music "Pascual: España Cañí Pasodoble" to set the vibe.

{{< youtube FCLIuzS64ms >}}

> In a bullring, a brave matador is engaged in a splendid fight with a furious bull. The matador is agile, meaning that he can change his velocity **immediately** (even at accelerations up to 100g), but he has a **maximum velocity**. In contrast, the bull has **no upper limit** on its **velocity**, but it has a **maximum acceleration** due to its massive build. The bull wants to gore the matador while the matador wants to dodge the bull’s charge. Can the bull knock down the matador in a finite time? Or can the matador always dodge the bull’s charge for as long as he wants?
> **Note**: we model both the matador and the bull as a point without volume.

*Scroll down the see the answer.*

{{< rawhtml >}}
<div style="height: 1000px;"></div>
{{< /rawhtml >}}

---

# Answer

The matador has a strategy to dodge the bull's charge forever. The intuition is that when the bull is moving at a low velocity, the matador can maintain a safe distance by moving along a circular path. When the bull charges at a high velocity, the matador can execute an emergency dodge at the last possible moment. Because the bull cannot alter its course quickly in time, it misses the matador and the overshoots create a crucial gap. The matador seizes the opportunity to run back to his circular path so that he can continue the evasion.

## Details

| Notation | Meaning |
| --- | --- |
| $\bar v_m$ | maximum velocity of the matador | 
| $\bar a_b$ | maximum acceleration of the bull |
| $v_m$ | current velocity of the matador |
| $v_b$ | current velocity of the bull|
| $t$ | current time ($t=0$ is the beginning of the fight) |
| $d_0$ | original distance between the matador and the bull |
| $d$ | current distance between the matador and the bull |
| $M$ | point representing the matador |
| $B$ | point representing the bull |
| $D(a,r)$ | an open disk centered of radius $r$ about $a$|

For brevity, phrases like "the matador moves," "runs," or "dodges" imply he is moving at his maximum speed, $\bar v_m$.

Suppose there exists $R > 0$ such that $D (M, R)$ is an open set contained in
the bullring, otherwise move away from the edge in a very short time. Let $d'
= \min \left\{ \frac{\bar{v}_m^2}{2 \bar{a}_b}, d_0, \frac{1}{10} R \right\}$,
$r = \frac{1}{10} d'$, $\varepsilon_1 = \min \left\{ 1, 0.001 \frac{d'
\bar{a}_b}{\bar{v}_m^2} \right\}$, $\varepsilon = \min \left\{
\frac{\varepsilon_1 \bar{v}_m^2}{200 \bar{a}_b}, \frac{d'}{100} \right\}$,
$t_1 = \frac{\varepsilon}{0.9 \bar{v}_m}$, $t_2 = 0.9
\frac{\bar{v}_m}{\bar{a}_b}$. It's apparent that $2 t_1 < t_2$.

The matador's winning strategy is as follows: initially, the matador chooses a circle of radius $r$ about $O$ passing through his starting position. Constrain $\angle MOB \in [0,\pi]$. The strategy then alternates between two stages:
- **Escape stage**: When $d>\epsilon$, the matador runs along the circle in the direction that increases $\angle MOB$. When $\angle MOB = \pi$, the matador runs to maintain this maximum angle.
- **Dodge stage**: This stage is triggered when $d = \epsilon$, the matador immediately moves in the direction perpendicular to $v_b$ at this moment for $t_1$, then reverses direction and heads back for another $t_1$ to return to his starting point. After return to the circle $O$, the parador remains stationary for $t_2-2t_1$.

We assert that at the end of the dodge stage, $d>\epsilon$, which means the system re-enters the escape stage. The proof of perpetual survival now follows by considering two cases. During the fighting, if the matador enters the dodge stages infinitely many times, he survives forever because each dodge stage lasts for a non-zero duration $t_2$. If the matador only enters the dodge stage only a finite number of times, then he remains exclusively in the escape stage after sufficienly long time, which also means he can survive forever. This completes the proof.

We call an escape stage **good**, if $d > d'$ at the beginning of the escape stage. We call a dodge stage **good**, if at the beginning of the dodge stage, $v_b > 0.9 \bar v_m$.

Then we only need to prove the following properties:
1. The first escape stage is good.
2. The bull cannot hit the matador in an escape stage.
3. If a dodge stage follows a good escape stage, then it is good.
4. The bull cannot hit the matador in a good dodge stage if the matador follows the winning strategy.
5. If an escape stage follows a good dodge stage, then it is good.
6. Over the whole strategy, the matador is always in $D(O,R)$

Proof of 1&2: Trivial.

Proof of 3: We'll prove it by contradiction. Suppose $t_d$ is the time when $d
= \varepsilon$ and $v_b \leqslant 0.9 \overline{v}_m$. Let $t_e$ be the start
time of the last escape stage and $d_e = d (t_e)$. Let $\Delta t =
\frac{\varepsilon_1 \bar{v}_m}{\bar{a}_b}$. Turn back time for $\Delta t$.
Then the distance between the bull and the parador is at most
$$
\begin{eqnarray*}
  \varepsilon + 2 r + 0.9 \bar{v}_m \Delta t + 1 / 2 \bar{a}_b \Delta t^2 & <
  & \frac{d'}{100} + \frac{d'}{5} + 0.9 \bar{v}_m \frac{\varepsilon_1
  \bar{v}_m}{\bar{a}_b} + 1 / 2 \bar{a}_b \left( \frac{\varepsilon_1
  \bar{v}_m}{\bar{a}_b} \right)^2\\
  & < & d' / 2 + (0.9 \varepsilon_1 + 0.5 \varepsilon_1^2)
  \frac{\bar{v}_m^2}{\bar{a}_b}\\
  & < & d' / 2 + (0.9 \varepsilon_1 + 0.5 \varepsilon_1)
  \frac{\bar{v}_m^2}{\bar{a}_b}\\
  & < & d' / 2 + 1.4 \cdot 0.001 \frac{d' \bar{a}_b}{\bar{v}_m^2} \cdot
  \frac{\bar{v}_m^2}{\bar{a}_b}\\
  & < & d' < d_e,
\end{eqnarray*}
$$
which means it is impossible for a bull to approach within $D (M,
\varepsilon)$ at $t_e + \Delta t$. Therefore, $t_d - \Delta t > t_e$.

Consider $t \in [t_d - \Delta t, t_d]$, the maximum velocity of the bull is
$0.9 \bar{v}_m + \bar{a}_b \Delta t = (0.9 + \varepsilon_1) \bar{v}_m$. We
also have $| {\operatorname{OB}} | \geqslant r - \varepsilon - (0.9 \varepsilon_1) \bar{v}_m \Delta t$. So the angular velocity of the bull
about $O$ is no more than $\frac{(0.9 + \varepsilon_1) \bar{v}_m}{r -
\varepsilon - (0.9 + \varepsilon_1) \bar{v}_m \Delta t} < \frac{0.91
\bar{v}_m}{r - \frac{\varepsilon_1 \bar{v}_m^2}{200 \bar{a}_b} - 0.91
\frac{\varepsilon_1 \bar{v}_m^2}{\bar{a}_b}} < \frac{0.91 \bar{v}_m}{r -
\frac{0.001 d'}{200} - 0.91 \cdot 0.001 d'} < 0.99 \bar{v}_m / r$. On the
other hand, the angular velocity of the matador is $\bar{v}_m / r$. As long as
the matador follows our suggested strategy, $\mathrel{\angle}
{\operatorname{MOB}}$ increases faster than $0.01 \bar{v}_m / r$.
This creates more than $0.01 \bar{v}_m \Delta t / r$ angle from $t_d - \Delta
t$ to $t_d$, which means $\mathrel{\angle} {\operatorname{MOB}}>
0.01 \bar{v}_m \Delta t / r$ at time $t_d$. On the other hand, if $d (t_d) =
\varepsilon$, $\mathrel{\angle} {\operatorname{MOB}} \leqslant 2
\arcsin \frac{\varepsilon}{2 r} < 2 \frac{\varepsilon}{r}$ at $t_d$. However,
$2 \frac{\varepsilon}{r} = 0.01 \frac{\varepsilon_1 \bar{v}_m^2}{r \bar{a}_b}
< 0.01 \bar{v}_m \Delta t / r$, which leads to an contradiction.

{{< inline-svg "img/drawing_crop.svg" >}}

Proof of 4\&5: Since the this is a good dodge stage, we have $v_b > 0.9
\bar{v}_m$. Let $t_d$ be the beginning of the dodge stage, $v_{b d} = v_b
(t_d)$. As shown in the figure above, we have
$$
\begin{eqnarray*}
  d (t_d + \Delta t) & \geqslant & \sqrt{(l_1 - v_{b d} \Delta t)^2 + (l_2 +
  \bar{v}_m \Delta t)^2} - \frac{1}{2} \bar{a}_b \Delta t^2\\
  & \geqslant & \bar{v}_m \Delta t - \frac{1}{2} \bar{a}_b \Delta t^2\\
  & \geqslant & \Delta t \left( \bar{v}_m - \frac{1}{2} \bar{a}_b
  \frac{\varepsilon}{0.9 \bar{v}_m} \right)\\
  & \geqslant & \Delta t \left( \bar{v}_m - \frac{1}{2} \bar{a}_b
  \frac{\frac{d'}{100}}{0.9 \bar{v}_m} \right)\\
  & > & 0
\end{eqnarray*}
$$
when $\Delta t \leqslant t_1$, and
$$
\begin{eqnarray*}
  d (t_d + \Delta t) & \geqslant & \sqrt{(v_{b d} \Delta t - l_1)^2 + (l_2 +
  \bar{v}_m (2 t_1 - \Delta t))^2} - \frac{1}{2} \bar{a}_b \Delta t^2\\
  & \geqslant & \sqrt{(0.9 \bar{v}_m \Delta t - \varepsilon)^2 + ( \bar{v}_m
  (2 t_1 - \Delta t)) ^2} - \frac{1}{2} \bar{a}_b \Delta t^2\\
  & \geqslant & \frac{0.9 \bar{v}_m \Delta t - \varepsilon + 0.9 (\bar{v}_m
  (2 t_1 - \Delta t))}{\sqrt{1^2 + 0.9^2}} - 2 \bar{a}_b t_1^2\\
  & \geqslant & 1.2 \bar{v}_m t_1 - 0.8 \varepsilon - 2 \bar{a}_b t_1^2\\
  & = & 1.2 \frac{\varepsilon}{0.9} - 0.8 \varepsilon - 2 \bar{a}_b \left(
  \frac{\varepsilon}{0.9 \bar{v}_m} \right)^2\\
  & \geqslant & 0.53 \varepsilon - 2 \frac{\varepsilon
  \bar{a}_b}{\bar{v}_m^2} \cdot \frac{d'}{100}\\
  & \geqslant & 0.53 \varepsilon - 2 \frac{\varepsilon
  \bar{a}_b}{\bar{v}_m^2} \cdot \frac{\bar{v}_m^2}{2 \overline{00 a}_b}\\
  & > & 0
\end{eqnarray*}
$$
when $t_1 < \Delta t \leqslant 2 t_1$, and
$$
\begin{eqnarray*}
  d (t_d + \Delta t) & \geqslant & \sqrt{(v_{b d} \Delta t - l_1)^2 + l_2^2} -
  \frac{1}{2} \bar{a}_b \Delta t^2\\
  & \geqslant & 0.9 \bar{v}_m \Delta t - \varepsilon - \frac{1}{2} \bar{a}_b
  \Delta t^2\\
  & \geqslant & - \frac{1}{2} \bar{a}_b \left( \Delta t - 0.9
  \frac{\bar{v}_m}{\bar{a}_b} \right)^2 + 0.99 \frac{\bar{v}_m^2}{2 \bar{a}_b} \varepsilon\\
  & \geqslant & - \frac{1}{2} \bar{a}_b \left( \frac{2 \varepsilon}{0.9
  \bar{v}_m} - 0.9 \frac{\bar{v}_m}{\bar{a}_b} \right)^2 + 0.99
  \frac{\bar{v}_m^2}{2 \bar{a}_b} - \varepsilon\\
  & \geqslant & 2 \varepsilon - \varepsilon - \frac{2 \varepsilon 
  \bar{a}_b}{0.99 \bar{v}^2_m} \varepsilon\\
  & \geqslant & \varepsilon - \frac{{d'}  \bar{a}_b}{50 \bar{v}^2_m}
  \varepsilon\\
  & > & 0
\end{eqnarray*}
$$
when $2 t_1 < \Delta t \leqslant t_2$.

In summary, when $t \in [t_d, t_d + t_2]$, $d (t) > 0$. Moreover, we have
$$
\begin{eqnarray*}
  d (t_d + t_2) & \geqslant & 0.9 \bar{v}_m t_2 - \varepsilon - \frac{1}{2}
  \bar{a}_b t_2^2\\
  & = & 0.54 \bar{v}_m^2 / \bar{a}_b - \varepsilon\\
  & \geqslant & 1.08 d' - 0.01 d'\\
  & \geqslant & d',
\end{eqnarray*}
$$
which proves 5.

Proof of 6: Obvious in the escape stage. In the dodge stage, we have
$$
\begin{eqnarray*}
  | {\operatorname{OM}} | & \leqslant & r + t_1 \bar{v}_m\\
  & \leqslant & \frac{1}{100} R + \frac{\varepsilon}{0.9}\\
  & \leqslant & R
\end{eqnarray*}
$$

Q.E.D.

**Another question**:

> Given an arbitrary open set in the bullring, can the matador move towards and finally step on this area while dodging the bull's charger?

{{< collapse summary="Hint (click to expand/collapse)" >}}
Yes. Select an arbitrary smooth path from the matador's original place to the destination. Let the matador move along the continuous path at a velocity less than $\bar v_m/2$ and an acceleration less than $\bar a_b/2$. Adding the velocity to the strategy of "a parador with a maximum speed of $\bar v_m/2$ has a winning strategy over a bull with a maximum acceleration of $3\bar a_b/2$ within an arbitrarily small region" according to the last subsection gives our winning strategy because the matador only deviates from its path a tiny distance. We can let the tiny distance much less than the diameter of our destination of open area.

{{< /collapse >}}

# Afterword

After writing up the proof, I sent my text to AI for proofreadng. The AI pointed out that this problem falls under the catagory of [homicidal chauffeur problems](https://en.wikipedia.org/wiki/Homicidal_chauffeur_problem). It’s frustrating to realize I’ve unknowingly reinvented a historical theorem—but at least the process of proving it was fun.
