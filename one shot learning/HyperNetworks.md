# Hypernetworks

Ha, David, Dai, Andrew, and Le, Quoc V. Hypernetworks.International Conference on Learning Representations (ICLR), 2017.

> 学习如何动态更新循环网络，用一个小网络(Hypernetwork)生成一个大网络(a main network)的权重。

<div align="center">
<img src="https://i.loli.net/2018/05/03/5aeaa6339b74f.png"  />
</div>

这容易让人联想到神经进化学，但是我们的网络是端到端用梯度下降与main network一起进行训练的，显然更高效。

本文的灵感来源于进化计算，进化计算很难直接处理有数百万计的权重参数待优化的情况。所以一个更高效的方法是进化一个较小的网络来学习一个较大的网络的权重结构。这样搜索范围就被限制在一个较小的权重空间了。

我们的重点在于为mian network生成权重，比如将特征向量作为输入可以为卷积网络，循环网络等生成权重，将坐标输入网络也可以为全连接网络产生权重，就像DPRNs（HYPERNEAT神经进化）。

## 对比卷积网络与循环网络

我们认为卷积网络与循环网络是两个极端：循环网络各层之间的权重是共享的，这样并不灵活且因为梯度消失而难以学习。卷积网络的每一层内的参数是共享的，但层与层之间参数不共享增加了网络的灵活性，但是当网络加深时也存在大量的冗余参数。Hypernetwork可以看做是一种放宽了的权重共享，因此在这两个极端中取得了一个平衡。

## 静态超网络->深度卷积网络

用一个超网络学习主网络的**各层**权重，其输入是各层的feature map，输出是该层的权重kernel参数。超网络的结构是一个两层的线性映射。如下图所示：

<div align="center">
<img src="https://i.loli.net/2018/05/03/5aea7ce2c92fb.png"  />
</div>

两层线性映射：

<div align="center">
<img src="https://i.loli.net/2018/05/03/5aea7d1027589.png"  />
</div>

## 动态超网络->循环网络

<div align="center">
<img src="https://i.loli.net/2018/05/03/5aeaa6a79b7d5.png"  />
</div>