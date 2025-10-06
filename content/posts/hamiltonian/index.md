---
title: "Hamiltonian from the Perspective of Order Reduction"
date: 2025-10-06T08:57:27+08:00
draft: false
---

The transition from the Lagrangian to the Hamiltonian formulation can be viewed as an operation that reduces a higher-order dynamical system to a first-order one. Specifically, given the Euler–Lagrange equation  
\[
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_i}\right) - \frac{\partial L}{\partial q_i} = 0,
\]
let  
\[
p_i = \frac{\partial L}{\partial \dot{q}_i}.
\]
Then we have  
\[
\dot{p}_i = \frac{\partial L}{\partial q_i}.
\]
We would also like to introduce an equation that describes the evolution of \( q_i \):  
\[
\dot{q}_i = \dot{q}_i(q_i, p_i, t) := v(q_i, p_i, t).
\]
At this point, the reduction of order has, in essence, been accomplished. However, physicists often prefer to express formulas in a more compact and aesthetically appealing manner, ideally in the form of a higher-dimensional dynamical system (recall from control theory that such systems are mathematically more tractable).  

Since we already have \( p_i = \frac{\partial L}{\partial \dot{q}_i} \), we aim to obtain a formulation of the form  
\[
\dot{\mathbf{z}} = J \, \nabla_{\mathbf{z}} H(\mathbf{z}, t),
\]
where  
\[
\mathbf{z} =
\begin{pmatrix}
q_1 \\ \vdots \\ q_n \\ p_1 \\ \vdots \\ p_n
\end{pmatrix}.
\]

To explore this idea, let us begin with the simplest case \( n = 1 \). If the construction does not work in the one-dimensional case, it is unlikely to generalize successfully to higher dimensions. We would like \(\nabla H\) to contain terms such as \(\frac{\partial L}{\partial q_1}\) and either \(v\) or \(\dot{q}_1\)—or at least their linear combination. This goal can be achieved easily by defining  
\[
H_1 = L(q_1, \dot{q}_1, t) + p_1 \dot{q}_1.
\]
Why not instead define  
\[
H_2 = L(q_1, \dot{q}_1, t) + p_1 v(q_1, p_1, t)?
\]
Is there any difference between these two choices? Indeed, this involves a small mathematical trick often employed by mathematicians when performing *gradient detaching* (see [link](https://bnikolic.co.uk/blog/pytorch-detach.html)):  
\[
\frac{\partial H_1}{\partial q_1} = \frac{\partial L}{\partial q_1},
\quad\text{whereas}\quad
\frac{\partial H_2}{\partial q_1} = \frac{\partial L}{\partial q_1} + p_1 \frac{\partial v}{\partial q_1}.
\]
After adopting \(H_1\), we can set  
\[
J_1 =
\begin{pmatrix}
0 & I \\
I & 0
\end{pmatrix}.
\]

In practice, the Hamiltonian is defined as  
\[
H(q_i, p_i, t) = \sum_{i=1}^{n} p_i \dot{q}_i - L(q_i, \dot{q}_i, t),
\]
which differs from the above only by a sign; the essential structure remains the same. The sign convention is chosen so that the expression aligns with the Legendre transform.

**Remark 1.** From a personal perspective, this viewpoint provides a more compelling motivation than the conventional approach of “directly applying the Legendre transform to the Lagrangian action and then discovering, almost miraculously, that the transformed variables \(p\) and \(q\) constitute a first-order dynamical system.” Of course, if anyone can clarify the underlying reason behind this “miracle,” I would be very grateful.  
