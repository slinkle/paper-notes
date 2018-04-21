# Siamese Neural Networks for One-shot Image Recognition
 G Koch, R Zemel, and R Salakhutdinov. Siamese neural networks for one-shot image recognition. In ICML Deep Learning workshop, 2015.
 
孪生网络 **Siamese Neural Network**,衡量两个输入的相似度。当网络训练完成后，我们可以直接利用网络的超强特征实现对未知分布新样本数据的泛化识别。

训练一个网络实现对两张图片相似度的判别，当输入新图片时，从图片库中寻找最相似的作为分类。

<div align="center">
<img src="https://i.loli.net/2018/04/20/5ad99d7b21d95.png"  />
</div>

## 网络介绍

孪生网络最早是为了解决签名验证作为图像匹配问题引入的[Bromley and LeCun, 1990s]。该网络接收两个完全不同的输入并分别计算出高层次特征，然后再利用一个能量方程计算距离。这两路网络的参数是被绑定为完全相同的。这样可以保证两个十分相似的输入在映射到高维特征空间后不会相距太远，因为两路网络的映射方程是一样的。而且网络结构是对称的，这是十分必要的，因为x1到x2的距离与x2到x1的距离应该相同。也就是说，如果颠倒两张输入图片的顺序，输出的概率是相同的。让两个输入通过**完全相同，共享参数**的网络，然后使用绝对差分作为线性分类器的输入--这是孪生网络必须的结构。两个完全相同的双胞胎，共用一个头颅，这就是孪生网络的由来。

<div align="center">
<img src="https://i.loli.net/2018/04/20/5ad99bd8e443b.png"  />
</div>

不同于LeCun等使用[**对比损失**](https://blog.csdn.net/autocyz/article/details/53149760)作为相似度度量，我们直接使用带权重的L1距离结合sigmod激活函数再加上交叉熵计算损失。

<div align="center">
<img src="https://i.loli.net/2018/04/20/5ad9a0cdf0e38.png"  />
</div>

## 模型

我们定义一个孪生网络模型，使用两个输入层来调用它，这样两个输入使用相同的参数。然后我们把它们使用绝对距离合并起来，添加一个输出层，使用二分类交叉熵损失来编译这个模型。

## 讨论

实现的是一个相似度度量学习，因为输入是两张图像对，所以训练数据很大，不太容易过拟合（虽然实际上也出现过拟合问题）。但是这样的机制导致，输入一张测试图片，与训练集中的图片进行对比，可能有不止一张相似度很高的图片，缺乏唯一性，从而降低分类的可信度。也就是说，训练目标和测试目标是不同的，训练目标是度量两张图片的相似度，而测试是为了找出测试图片的类别。

摘自https://sorenbouma.github.io/blog/oneshot/

> Matching Networks for One Shot learning 这篇论文就是做这个的。它们使用深度模型来端到端的学习一个完整的近邻分类器，而不是学习相似度函数，直接在单样本任务上训练，而不是在一个图像对上。Andrej Karpathy’s notes 很好的解释了这个问题。因为你正在学习机器分类，所以你可以把他视为元学习（meta learning）。

> One-shot Learning with Memory-Augmented Neural Networks 这篇论文解释了单样本学习与元学习的关系，它在Omniglot数据集上训练了一个记忆增强网络，然而，我承认我看不懂这篇论文。
