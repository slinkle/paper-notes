# Model-Agnostic Meta-Learning for Fast Adaptation of Deep Networks

Chelsea Finn, Pieter Abbeel, and Sergey Levine. Model-agnostic meta-learning for fast adaptation of deep networks. *Proceedings of the 34th International Conference on Machine Learning 2017.

**模型无关自适应 元学习

本文提出的方法可以适用于任何用梯度下降训练的模型，可用于多种不同的学习任务上，包括分类、回归和强化学习。

meta-learning的目标是在各种不同的学习任务上训练出一个模型，使之可以通过少量的学习样本在解决一个新的任务。本文的方法可以在少样本情况下，通过少量的迭代次数，在新的任务上获得很好的泛化性能，而且非常容易进行fine-tune。这个方法无需关心模型，也不需要为meta learning 增加新的参数，直接用梯度下降来训练leaner。

本文的关键思想是学习模型的初始参数使之在面对一个新任务，仅有少量样本，通过一次或者几次迭代后可以获得最优的性能。它学习的不是模型参数的更新函数或学习规则，也不会增加学习参数，或者为学习模型增加约束。本质上学习一种最优的特征描述，只要提取的中间特征能够适应于各种任务，那么在面临新任务时只需要将最顶层的权重进行微调就可以得到较好的结果。也可以说我们学习的过程实际上是最大化损失函数的敏感度的过程，也就是说当局部参数发生一点变化的时候，就能引起相关任务的损失函数性能发生巨大的提升。

## Meta-Learning Problem Set-Up

在meta-learning阶段我们通过一个任务集来训练一个model/leaner，使之可以迅速适应新任务。在训练时，一整个任务被当作一个训练样本。

<div align="center">
<img src="https://i.loli.net/2018/05/01/5ae7e36858c33.png"  />
</div>
