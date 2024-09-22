---
title: "Brainstorm"
date: 2023-03-16T22:52:59+08:00
draft: False
tags: ["idea", "perspective"]
categories: ["AI"]
---

Here are some immature ideas that I come up with when I am taking a walk or
having a meal. Feel free to get some inspiration from this post and write some
papers. I am glad to see study on these topics. This post will be updated from
time to time.

1. The research field underestimates the importance of optimization. You cannot
   expect one to have perfect memory. What we do every day is just adjusting our
cognition. That's what [Mass Editing Memory in a
Transformer](https://memit.baulab.info/) does! This method remodels knowledge,
namely the relation between object. But it does not involve behavioral
remodeling, for example the procedure to solve a tedious math problem.
Information of relations between texts and images is in cross-attention
layers(e.g. prompt to prompt), while the knowledge-related relations are stored
in MLP layers(e.g. https://rome.baulab.info/). Are procedural relations stored
in cross-attention layers?

3. Humans can induct rules given miscellaneous facts. The rules can be
   utilized for robust and efficient judgement.

4. Human is able to transfer to the relation of open-world objects as long as he
   or she has realize such concept, even if the sample is simple. For example a
child can learn the relative spatial concept of "left" and "right" by observe
the position of building blocks a teachers shows. From such a point of view,
humans is capable of separating the learning process of objects and relations.
However, the models learn visual representation from the whole image. They can
hardly transfer to the concept of "A on B" if "A" and "B" are new objects
although they have learned some scenes having the concept of "on".(TODO: really?
perform an experiment!)(THOUGHTS: perhaps we can separate structure and
objects?)(THOUGHTS: can we save some patterns, or typical examples in memory and
retrieve the pattern in inference like what we do in few shot learning.)
Incremental span relation?

5. Learning cycle (which can easily solve long-tail problem):
   Leaning(connectionism) -> summary and extract rule(symbolicism) -> use rules
and internalization(connectionism)(use rules = in-context learning-derived
pseudo label)

6. Perhaps different people deal with information in different ways (in images,
   in texts, in voices, etc.) Does this mean the universal embedding in our
brain has a preferable modal which is different for peoples? What is your
preponderant subject? Math, Chinese, English...?

7. AGI becomes a general platform. Whenever domain-specific knowledge is
   required, we can add some payload to it. How to make the payload easy to add
or remove?

8. How does human store knowledge. Can we utilize the same approach in AI?

9. The depth of the network layer is a constant over the training process. Can
   we make it dynamic?

10. VLMO first trains MHSA and visual FFN on image-only data. Then it frozes
    MHSA and trains language FFN on text-only data. Why is it such an order? I
think language is easier than image and have more explicit semantic information.
So shouldn't it be trained first?

11. Can the model be more robust if we limit the bandwidth like what it is when
    the information is passed from the retina to the brain? It may keep the
model from adversarial attacks. Limited bandwidth but can see multiple times.

12. Math calculation through Reinforcement learning. Think of the world as a
    piece of infinite graph paper. Every block on it has a letter/word in. Then
the model reads and write the paper. In math calculation, it is easier to align
in the paper.

13. "Integration is everything" biology paper:
    https://www.science.org/doi/10.1126/science.1238411

14. Part predicts part instead of considering the global influence using back
    propagation.

15. Ultimate model

- Entangled components specifically suitable for different sub-tasks(brain
  partition)
- Embodied intelligence
- Corresponding parameter updating method
- Corresponding Training strategy
- Quantum acceleration(?)
- Deeply intra-entangled and shallowly interactive

17. Codewords are a universal language. Hierarchical predictive coding
    architecture.

18. How to measure the memory capability of a model for different models
    including CNN, RNN and Transformer?

19. How to symbolize a neural network? Quantization?

20. What's the utilization rate of a neuron? How to measure the expressive
    ability of models and the complexity of data?

21. Combine "pruning is learning" in the lottery ticket hypothesis and
    "forgetting is learning" in the information bottleneck theory together.

22. Similarity between circuits in different networks?

23. Adversarial attacks towards circuit? Hallucination.

24. To what extent does the model rely on rote memorization? In model training,
    two forces contribute to performance improvement: rote memorization and the
development of circuits (genuine understanding of patterns). Rote memorization
does not benefit performance on the test set much, whereas circuits, which
represent a deeper understanding, offer stronger generalization capabilities. I
am curious if there is a way to reduce the model's reliance on rote memorization
while enhancing the development of circuits. The first step would be to
quantitatively assess these two abilities and disentangle them from the
performance curve on the test set.

25. Language is meant to be used, not merely parroted. The true measure of a
    language model's generation quality lies in assessing the effectiveness and
efficiency of communication in practical application scenarios. This is why
instruction tuning and reinforcement learning from human feedback (RLHF) are so
crucial. However, both methods heavily rely on human intervention and require
significant labor and resources. In fact, placing an intelligent agent in an
interactive environment that provides feedback can simulate the scenarios in
which humans use language. Since this environment provides feedback, the results
can be used to assess communication effectiveness, or in other words, serve as a
reward, becoming the supervisory signal for reinforcement learning.

26. Does a fine-tuned model exhibit stronger hallucinations? How to identify and
    address hallucinations? How to modify internal pathways?

27. SGD is not the best optimization algorithm for neural networks. Is there
    better algorithms? Can you prove the disadvantages of SGD? Analyze a simple
(Hierarchical) model trained on structured synthetic dataset using SGD.
Prove/verify that it would converge to a suboptimal point.

28. As shown in [this
    blog](https://www.borealisai.com/research-blogs/neural-tangent-kernel-applications/)
, the parameter might remain constant when the loss decreases because the change
on parameters is distributed over thousands of millions of parameters.
Dispersing knowledge to a large number of parameters makes it more vulnarable to
unrelated information which could result in hallucinations. This innate property
in dense neural networks varies a lot with biological brains. Perhaps we need
sparse connection? Can you prove it?
