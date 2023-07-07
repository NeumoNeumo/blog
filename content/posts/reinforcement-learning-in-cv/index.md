---
title: "Reinforcement Learning in Captioning"
date: 2022-08-22T14:13:57+08:00
draft: true
---

In this blog, I am going to introduce some applications of reinforcement
learning in captioning with my ideas and thoughts included.

# Brief Introduction
In RL (Reinforcement Learning), an agent is expected to perceive the environment
and take corresponding actions to maximize its reward in the long run. It is a
continual interaction with the world compared with other machine learning
methods where the external information only feed into the model once, such as
CNN and Transformer. On account of the similarity between reinforcement learning
and the creatures in the nature (including humans), applying reinforcement
learning into deep learning to get more intelligent performance is quite
promising.

Captioning is a multi-modal task in which a model should automatically generate
a proper and accurate description for a given picture. The model is required not
only to understand visual information but to have a good command of language as
well, thus making it challenging for machine learning.


# Draft
## Previous work without RL
### Fill Caption Templates
Use the results of object detection and attribute discovery to fill predefined
caption templates.

**Cons**:
- Time-consuming
- Lacking in generability across different data distribution
- Insufficient support to complex sentences

### Image Retrieval
First retrieve similar pictures from an image-text pair database and then
integrate and modify these texts to match the given picture.

**Cons**:
- High space occupancy due to the database
- Theoretical performance upper bound is limited by the dataset

### Encoder-Decoder Framework
In this framework, the picture first forward propagates through a visual
network, e.g. CNN, and then the visual features are fed into a recurrent neural
network to "translate" an image to a sentence.

**Cons**:
- Potential information loss in deep neural networks

## RL Models in Captioning
> Show, Attend and Tell: Neural Image Caption Generation with Visual Attention (ICML 2015)

Imagine what we will do when we are writing a caption for a picture, especially
when there are many objects in the picture? 
<!-- {{< figure src="img/2022-08-28-17-22-47.png" caption="Steve Francia" align="center">}} -->
![](img/2022-08-28-17-22-47.png "Source: http://proceedings.mlr.press/v37/xuc15.pdf")


In this picture, we first notice a giraffe and the giraffe is in the forest. So
we may say "A giraffe standing in a forest with trees in the background".
Retrospect what we did just now. We first saw salient objects and then our focus
moved to other things to make the description more detailed.

Inspired by the "attention mechanism", the researchers propose an attention
based caption model.

> Deep Reinforcement Learning-Based Image Captioning With Embedding Reward (CVPR 2017)

The goal of captioning is to generate a whole sentence matching the given
picture as much as possible. However, in encoder-decoder framework, the sentence
is generated word by word with a probability function $p(w_n |
w_{n-1},w_{n-2},\dots,w_1)$, making the model myopic and ignore more accurate
sentence in the long run. Although many methods, e.g. beam search and pruning,
have been proposed to alleviate the "greedy" tendency, this problem is an
intrinsic issue in encoder-decoder framework.

However, an RL model is meant to gain an overall discounted high reward which
naturally tackle the short-sighted defect. So here comes this paper.

To be specific, we regard the given image and the words predicted until now as
states and think of selecting the next word as actions. This model is comprised
of two parts

