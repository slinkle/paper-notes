# One-shot Learning with Memory-Augmented Neural Networks

Santoro, Adam, Bartunov, Sergey, Botvinick, Matthew, Wierstra, Daan, and Lillicrap, Timothy. Meta-learning with memory-augmented neural networks. In International Conference on Machine Learning (ICML), 2016.

## 元学习

参考博客[https://blog.csdn.net/mao_feng/article/details/78939864]

它属于基于**元学习**(meat-learning)的少样本学习：  通过大量的数据，现在的AI系统能从0开始学习一个复杂的技能。我们希望AI系统能获得多种技能并能适应各种环境，但针对每种技能都从0开始训练是无法承受的。因此，我们希望它能够**从之前的经验快速地学习新的技能**，而不是把新的任务孤立地考虑。这个方法，我们称为元学习（learning to learn,或meta learning）, 使得我们的系统在它的整个生命周期中可以持续地学习各种各样的任务。

<div align="center">
<img src="https://i.loli.net/2018/04/26/5ae146498eb4b.png"  />
</div>

<div align="center">
<img src="https://i.loli.net/2018/04/26/5ae1465bc080e.png"  />
</div>

<div align="center">
<img src="https://i.loli.net/2018/04/26/5ae146ee32343.png"  />
</div>

## 递归记忆模型

深度神经网络在遇到新数据时需要重新学习网络的参数.增加了外部存储(external memory)的神经网络图灵机Neural Turing Machines(NTMs)可以学习将知识表达存入记忆的策略，并学习如何使用这些表达来对新数据进行预测。本文基于NTMs的思想，结合外部存储可以快速准确预测那些只出现过一次的数据。
