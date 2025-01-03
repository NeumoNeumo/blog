---
title: "Thoughts on IQ"
date: 2025-01-03T15:11:27+08:00
draft: false
---

Does IQ matter in terms of test score? Yes. But recently, upon deeper
reflection, I come to realize that IQ is not the only factor that affects one's
exam performance.

# My Childhood

When I was in the third year of junior high school, I stumbled upon the Math
olympics by chance. It was then that I realized that all the math I had learned
was so naive and boring up to that point seemed -- it felt like it was only for
test, for scoring higher rather than for challenging human's talent and intelligence.
I've always loved puzzle games like Sokoban, Cut the Rope, Where's My Water, etc. 
For me, the visual effects in video games matter far less than the ingenious
level design and mechanics.
 You might guess that I am a fan of redstone mechinery in Minecraft. -- and
 you'd be right. In my perspective, Math felt like the perfect game: no flashy
 or gaudy visuals, just clever, sometimes obscure tricks to solve problems.
I'd often sit for an entire day trying to crack a tough problem.
And when
I finally solved it, it was a sheer bliss.

After immersing myself in Math for a
year, I earned a Provincial First Prize in High School Mathematics League in
Jiangsu province. It seemd that I was on track to join the provincial
team, compete in Chinese Math Olympiad(CMO) in the coming years 
and potentially secure admission to a top university in China.

However, the following year, I made almost no progress in my score in the
League. By the time I was in my second year of high school, I received the
lowest score in the first part of the competition (see note). Ultimately, I
wasn’t invited to join the provincial team and ended up attending the Southern
University of Science and Technology (SUSTech).

> The League score is divided into two parts. The first part is relatively
> easier, worth 120 points, while the second part is more challenging, worth 180
> points. Some students score over 100 in the first part but end up with 0 in
> the second part.

When I was a junior high school student, I didn’t consider myself a genius, but
I didn’t think I was stupid either, as I consistently achieved decent scores
among participants my age. However, as I grew older, I began to doubt whether I
had a true knack for math. This was evident in my ever-declining scores in the
League. My doubts were further amplified by an incident where I spent days
struggling with a problem, only to watch a member of the Chinese national Math
Olympics team solve it in seconds. I started to blame my failures on my
supposedly low IQ.

# Problem Solving as a Path Search Problem

Solving a math problem is like navigating a carefully designed path, where each
step must adhere to the given rules of inference. The problem provides a
starting point and requires you to reach a specific destination. To find the
solution, you can work forward from the starting point, exploring the properties
and implications of the given conditions, or work backward from the destination,
identifying the necessary conditions to achieve the goal. When these two
approaches intersect, a valid path emerges. However, the space of possible
states is vast, so an efficient heuristic search strategy is essential to
identify the correct path within a limited time.

In the context of Large Language Models, we might call the path search as Chain
of Thoughts(CoT) or its variants like Tree of Thoughts(ToT).

During the training phase, the model learns from a set of problems and their
corresponding solutions. It trains a heuristic search network and can memorize
typical problems and their solutions for Retrieval-Augmented Generation (RAG).
However, it is unlikely to encounter the exact same problem in the dataset, and
even problems that use similar methods may vary significantly in their
formulation. To address this, the model might decompose its knowledge into
fundamental topics, such as "tricks for applying the minimum principle" or
"strategies for using the pqr method in inequalities." Despite this, the model
may still struggle to retrieve relevant data if the connection between the
current problem and these basic topics is unclear.

To improve this, the model is expected to build a network of interconnected
basic topics. Each concept would be linked to multiple typical problems, and
each problem in the dataset could be categorized under multiple basic topics.
This structure would enhance the model's ability to retrieve and apply relevant
knowledge effectively.

In the testing stage, the model identifies potential related basic topics by
analyzing the conditions of the problem. It then retrieves relevant problems
associated with those topics. Augmented by these related problems and the
model's own knowledge, it is expected to generate a solution to the problem.

# Retrospection

I love math because it is fascinating. I enjoy the freedom of exploring the
infinite, unknown space of problem-solving. However, this alone is not enough to
guarantee a good test score. Exams are time-constrained, and a systematic,
efficient approach to finding solutions is crucial. I never built my own
knowledge network, so no matter how many problems I practiced, I was only
training my path-searching module without incorporating Retrieval-Augmented
Generation (RAG) or more advanced techniques. A machine learning model can train
in a virtual world for what amounts to hundreds of years, just to match the
path-searching ability of a human expert. But I don’t have that much time or
energy. To make matters worse, my excessive love for novelty and unconventional
problems filled my training with data that fell outside the distribution of
typical test problems. It’s no surprise that I ended up with my worst score in
my third attempt.

In short, the idea of prioritizing IQ above all else, without making meaningful
changes to my learning methods, was a way of masking strategic laziness with
tactical diligence. Blaming my struggles on a vague and insurmountable issue was
like an ostrich burying its head in the sand. To my high school self from years
ago, I would say: think from a higher perspective rather than relying solely on
hard work. As an old Chinese saying goes, "富在术数不在劳身，利在势局不在力耕" —
"Wealth lies in strategy, not in physical labor. Success lies in positioning,
not in sheer effort."
