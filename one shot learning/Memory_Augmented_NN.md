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

元学习一般有两级，一级是任务内的学习，即快速地获得每个任务中的知识，一级是跨任务的学习，即较慢地提取所有任务中学到的不同类型的任务和其要达到的目标之间的关联信息。这种模式也被称为 **learning to learn**.

结合记忆功能的神经网络可以很好的实现元学习的任务。这些网络通过权重的更新来shift their bias，并且学习将表征快速存储在记忆中来调节输出。然而，利用非结构化的循环神经网络的内部记忆单元无法扩展到需要对大量的新信息进行快速编码的任务上。因此，我们需要让存储在记忆中的信息的表达既稳定又能按元素进行访问。前者时说在需要时就可以可靠的访问到，后者是要求可选择性的访问相关的信息。另外，参数的数量不能被内存的大小束缚。LSTMs的存储单元并不能满足这两个条件。但是神经图灵机NTMs和记忆网络Memory Networks可以符合。所以我们提出了a highly capable memory-augmented neural network (MANN)，注意这里的记忆是通过外部存储实现的，而不是像LSTMs那样的内部存储。

本文的方法集成了两种方法的优势：一种是通过梯度下降对原始数据进行表征可以学到抽象的表达能力；一种是通过外部存储机制可以实现对新数据的快速表达和适应。

## 元学习方法论

通常，我们通过选择合适的参数 theta 使得针对某一数据集 D 的代价函数 L 达到最小值。但是在元学习任务中，我们是选择合适的参数 theta 使得符合某一分布 *P(D)* 的代价函数 L 的期望达到最小。

<div align="center">
<img src="https://i.loli.net/2018/04/26/5ae18a1aef205.png"  />
</div>

在输入数据给网络的时候，采取标签滞后的策略，在t时刻输入当前时刻的样本x_t和上一时刻的样本标签y_t-1,这样在t时刻是不知道样本x_t的标签的，需要自己预测再在下一时刻进行对比和损失计算，并在外部存储模块中储存样本编码和对应的标签信息，将这两者进行绑定，便于后续进行查询。同时，我们还希望通过这个过程学习到数据集的概率分布模型。

<div align="center">
<img src="https://i.loli.net/2018/04/26/5ae18e9db435b.png"  />
</div>

NTM可以通过缓慢更新权重来实现一个长时记忆，还可以通过外部存储进行短时记忆。它可以学习将信息表达存入记忆的策略，并如何利用这些表达进行预测。因此它可以实现对只见过一次的数据进行准确预测。

我们的模型分为控制器和外部存储器两部分，这两部分之间通过读写操作进行交互，读就意味着从记忆中读取表征，写就是将得到的表征存入记忆中。其中控制器可以是LSTMs或者是前馈网络。现在我们给出一个输入x_t,控制器会产生一个编码key_t,这个要么直接作为记忆矩阵M_t的一行被写入存储器中，要么用于从存储器中提取表征。在提取的过程中，我们寻找对应的记忆矩阵的某一行的标准是余弦相似度：

<div align="center">
<img src="https://i.loli.net/2018/04/26/5ae1d363f37e7.png"  />
</div>

依次遍历记忆矩阵的各行，得到key_t与每一行的相似度，用softmax计算出一个读取权重向量wr_t:

<div align="center">
<img src="https://i.loli.net/2018/04/26/5ae1d3eb57366.png"  />
</div>

接下来利用这个读取权重向量产生我们最终从记忆中提取的关于输入x_t的表征r_t:

<div align="center">
<img src="https://i.loli.net/2018/04/26/5ae1d4470a6fb.png"  />
</div>
