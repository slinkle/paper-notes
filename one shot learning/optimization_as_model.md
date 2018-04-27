# OPTIMIZATION AS A MODEL FOR FEW-SHOT LEARNING

Ravi, Sachin and Larochelle, Hugo. Optimization as a model for few-shot learning. In International Conference on Learning Representations 
(ICLR), 2017.

文章学习的是一个模型参数的更新函数或更新规则。它不是在多轮的episodes学习一个单模型，而是在每个episode学习特定的模型。具体地，基于梯度下降的参数更新算法，采用LSTM表达meta learner，用其状态表达目标分类器的参数的更新，最终学会如何在新的分类任务上，对分类器网络(learner)进行初始化和参数更新（优化）。

这个优化算法同时考虑到一个任务的短时知识和跨多个任务的长时知识。每个任务只有少量的更新，即我们希望通过少量的迭代，训练meta-leaner使得leaner在每个任务上收敛到一个好的解，从而使得这个优化算法能够拥有较好的泛化能力。

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
