# Model-Agnostic Meta-Learning for Fast Adaptation of Deep Networks

Chelsea Finn, Pieter Abbeel, and Sergey Levine. Model-agnostic meta-learning for fast adaptation of deep networks. arXiv:1703.03400, 2017.

模型无关自适应 元学习

本文提出的方法可以适用于任何用梯度下降训练的模型，可用于多种不同的学习任务上，包括分类、回归和强化学习。

meta-learning的目标是在各种不同的学习任务上训练出一个模型，使之可以通过少量的学习样本在解决一个新的任务。本文的方法可以在少样本情况下，通过少量的迭代次数，在新的任务上获得很好的泛化性能，而且非常容易进行fine-tune。

