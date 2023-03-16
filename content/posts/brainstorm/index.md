---
title: "Brainstorm"
date: 2023-03-16T22:52:59+08:00
draft: False
---

Here are some immature ideas that I come up with when I am taking a walk or
having a meal. This post will be updated from time to time.

1. We have retrieval-augmented models which retrieve image or text to enhance
   the prediction accuracy. However, data in the form of image and text are
   redundant. Much of the information is not necessary. For instance, we do not
   need to remember every pixel, actually. Therefore, I think remember what we
   have pre-encoded would be better. This process is similar to how humans
   memory works: only remember compressed concepts instead of details.
2. I think adjustment is more important than memory. You cannot expect one have
   perfect memory. What we do every day is just adjusting our cognition.
3. Information of relations between text and image is just in cross attention
   layers! (e.g. prompt to prompt)
4. human is can induct rules given miscellaneous facts. The rules can be
   utilized for robust and efficient judgement.
5. Human is able to transfer to the relation of open-world objects as long as he
   or she has realized such concept, even if the sample is simple. For example a
   child can learn the relative spatial concept of "left" and "right" by observe
   the position of building blocks a teachers shows. From such a point of view,
   humans is capable of separating the learning process of objects and
   relations. However, the models learns visual representation from the whole
   image. They can hardly transfer to the concept of "A on B" if "A" and "B" are
   new objects, although they have learned some scenes having the concept of
   "on".(TODO: really? Perform an experiment!)(THOUGHTS: perhaps we can separate
   structure and objects?)(THOUGHTS: can we save some patterns, or typical
   examples in memory and retrieve the pattern in inference like what we do in
   few shot learning.) Incremental span relation?
6. Learning cycle (which can easily solve long-tail problem):
    Leaning(connectionism) 
    -> summary and extract rule(symbolicism) 
    -> use rules and internalization(connectionism)
7. Perhaps different people deal with information in different ways (in images,
   in texts, in voices, etc.) Does this mean the universal embedding in our
   brain has a preferable modal which is different for peoples?
   What is your preponderant subject? Math, Chinese, English...?
8. AGI becomes a general platform. Whenever domain-specific knowledge is
   required, we can add some payload to it. How to make the payload easy to add
   or remove?
9. How human stores knowledge. Can we utilize the same approach in AI?
10. The depth of the network layer is a constant over the training process. Can
    we make it dynamic? 
