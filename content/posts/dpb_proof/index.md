---
title: "A Succinct Proof of Decoupled Parallel Backpropagation Convergence Lemma"
date: 2024-04-21T15:26:05-04:00
draft: false
categories: ["AI"]
tags: ["AI", "theory", "optimization"]
---

The meaning of the notations below complies with [the original
paper](https://arxiv.org/pdf/1804.10574.pdf).

$$
\begin{align*}
  \mathbb{E} [f (w^{t + 1})] - f (w^t) & \leqslant  \nabla f (w^t)^{\top}
  \mathbb{E} [(w^{t + 1} - w^t)] + \frac{L}{2} \mathbb{E} [\| w^{t + 1} - w^t
  \|^2]\\
  & =  - \gamma_t \nabla f (w^t)^{\top} \mathbb{E} \left[ \sum^K_{k = 1}
  \nabla f_{\mathcal{G} (k), x_i (t - K + k)} (w^{t - K + k}) \right] +
  \frac{L \gamma_t^2}{2} \mathbb{E} \left[ \left\| \sum^K_{k = 1} \nabla
  f_{\mathcal{G} (k), x_i (t - K + k)} (w^{t - K + k}) \right\|^2 \right]\\
  & =  - \gamma_t \| \nabla f (w^t) \|^2 - \gamma_t \nabla f (w^t)^{\top}
  \left( \sum_{k = 1}^K \nabla f_{\mathcal{G} (k)} (w^{t - K + k}) - \nabla f
  (w^t) \right) + \frac{K L \gamma_t^2}{2} \sum_{k = 1}^K \mathbb{E} [\|
  \nabla f_{\mathcal{G} (k), x_i (t - K + k)} (w^{t - K + k}) \|^2]\\
  & \leqslant  - \gamma_t \| \nabla f (w^t) \|^2 + \frac{\gamma_t}{2} \|
  \nabla f (w^t) \|^2 + \frac{\gamma_t}{2} \left\| \sum_{k = 1}^K \nabla
  f_{\mathcal{G} (k)} (w^{t - K + k}) - \nabla f (w^t) \right\|^2 + \frac{K^2
  L M \gamma_t^2}{2}\\
  & \leqslant  - \frac{\gamma_t}{2} \| \nabla f (w^t) \|^2 + \frac{K
  \gamma_t}{2} \sum_{k = 1}^K \| \nabla f_{\mathcal{G} (k)} (w^{t - K + k}) -
  \nabla f_{\mathcal{G} (k)} (w^t) \|^2 + \frac{K^2 L M \gamma_t^2}{2}\\
  & \leqslant  - \frac{\gamma_t}{2} \| \nabla f (w^t) \|^2 + \frac{K
  \gamma_t}{2} \sum_{k = 1}^K \| \nabla f (w^{t - K + k}) - \nabla f (w^t)
  \|^2 + \frac{K^2 L M \gamma_t^2}{2}\\
  & \leqslant  - \frac{\gamma_t}{2} \| \nabla f (w^t) \|^2 + \frac{K^2 L M
  \gamma_t^2}{2} + \frac{K L^2 \gamma_t}{2} \sum_{k = 1}^K \| w^{t - K + k} -
  w^t \|^2\\
  & \leqslant  - \frac{\gamma_t}{2} \| \nabla f (w^t) \|^2 + \frac{K^2 L M
  \gamma_t^2}{2} + \frac{K^4 L^2 M^2 \sigma \gamma_t^2}{2}\\
  & =  - \frac{\gamma_t}{2} \| \nabla f (w^t) \|^2 + \gamma_t^2 \frac{K^2 L
  M}{2} (1 + K^2 L M \sigma)
\end{align*}
$$
