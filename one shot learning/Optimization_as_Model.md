# OPTIMIZATION AS A MODEL FOR FEW-SHOT LEARNING

Ravi, Sachin and Larochelle, Hugo. Optimization as a model for few-shot learning. In International Conference on Learning Representations 
(ICLR), 2017.

文章学习的是一个模型参数的更新函数或更新规则。它不是在多轮的episodes学习一个单模型，而是在每个episode学习特定的模型。具体地，基于梯度下降的参数更新算法，采用LSTM表达meta learner，用其状态表达目标分类器的参数的更新，最终学会如何在新的分类任务上，对分类器网络(learner)进行初始化和参数更新（优化）。

这个优化算法同时考虑到一个任务的短时知识和跨多个任务的长时知识。每个任务只有少量的更新，即我们希望通过少量的迭代，训练meta-leaner使得leaner在每个任务上收敛到一个好的解，从而使得这个优化算法能够拥有较好的泛化能力。

<div>
<img src="https://i.loli.net/2018/04/27/5ae31a234e508.png"  />
</div>

## 模型

首先我们有一个神经网络leaner要学习一个分类或者回归任务。网络要更新的参数为theta。基于梯度下降的参数更新公式为：

<div align="center">
<img src="https://i.loli.net/2018/04/27/5ae281ba420b3.png"  />
</div>

我们对比发现，这个更新公式和LSTM的状态更新公式类似：

<div>
<img src="https://i.loli.net/2018/04/27/5ae283eb07341.png"  />
</div>

于是我们用LSTM的cell state表示leaner的参数theta，用candidate cell state c~ 表示梯度。这样我们就可以训练一个meta-leaner LSTM 来学习训练一个leaner神经网络的参数更新规则（避免神经网络通过大量的数据自己进行缓慢的梯度下降来更新参数）。

另外我们也将i_t(学习率)和f_t(忘记门)进行参数化，使其在参数更新过程中自动学习到最优值。

如公式所示，将学习率表示为当前参数、当前梯度、当前损失和上一次学习率的函数，由此，Meta leaner可以精细的控制学习率，从而可以快速的学习而不会发散。

<div align="center">
<img src="https://i.loli.net/2018/04/27/5ae2868e836d6.png"  />
</div>

f_t为忘记门，当learner陷入局部最优，即梯度为0但是损失很大，我们需要忘记之前的值，因此f_t的最优值不应该为常数1：

<div align="center">
<img src="https://i.loli.net/2018/04/27/5ae31b16e9f21.png"  />
</div>

另外我们还学习了LSTM的cell state的初值c0，将它看成meta-leaner的一个参数。这关系到meta-leaner要训练的分类器的权重的初值。这个初值的学习可以使meta-leaner决定leaner的权重初始值，从而使训练从一个较好的起点开始，使得优化能够快速进行。

## 训练

以训练miniImagenet数据集为例，训练过程中，我们从Dmeat-train的训练集（64个类，每类600个样本）中随机采样5个样本，每个类5个样本，构成训练集，去学习leaner；然后从Dmeat-train测试集的样本（64个类，每类剩下的样本）中采样构成测试集，集合中每类有15个样本，用来得到leaner的loss，去学习meta leaner。评估过程也是一样，我们从Dmeta-test的训练集（16个类，每类600个样本）中随机采样5个类，每个类5个样本，构成训练集去学习leaner；然后从Dmeat-test测试集的样本（16个类，每类剩下的样本）中采样构成测试集，每个类有15个样本，用来获得leaner的loss，去学习meta leaner。训练和测试过程在下图中用虚线分割：

<div align="center">
<img src="https://i.loli.net/2018/04/27/5ae320add83eb.png"  />
</div>

## 可视化

下图对meat-leaner的训练过程进行了可视化，把gate的值画出来，观察其在不同的数据之间是否存在变化。在1-shot上，meta-leaner学了10步，5-shot上学了5步。对于遗忘门，meta-leaner采用一个简单的权值衰减策略，而且每层都比较一致。输入门在不同数据上的变化比较大，说明meat-leaner没有采用一个固定的优化策略，而且1-shot和5-shot的表现也不同，说明meta-leaner对两者采用了不同的方法。如图：

<div align="center">
<img src="https://i.loli.net/2018/04/27/5ae322a5eb871.png"  />
</div>


