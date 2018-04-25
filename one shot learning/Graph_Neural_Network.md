# FEW-SHOT LEARNING WITH GRAPH NEURAL NETWORKS

Victor Garcia, Joan Bruna. Few-shot learning with graph neural networs. In International Conference on Learning Representations (ICLR), 2018.

提出了**graph neural network(GNN)** 图神经网络，基于Matching Network的思路，（将少样本学习转化为一个监督分类任务，学习一个从支持集的图片到对应标签的映射，并提出一个端到端的模型以感知机的形式接受支持集的输入）。我们将它改写为基于图的有监督学习任务，其中图的节点是集合中的图片，图的边是trainable similarity kernels(类似一种相似关系).基于当前的基于图结构的表征学习算法，提出了一种任务驱动的消息传递算法。

<div align="center">
<img src="https://i.loli.net/2018/04/25/5ae0892791dbf.png"  />
</div>

## 模型

少样本学习的目的是将标注图片的信息传递到未标注图片。这种信息的传递也可以理解为一种将已标注图片信息通过图模型完成的后验推断。

这篇文章并不直接学习一种两张图片的相似性度量，而是对匹配网络进行了扩展，将其感知机的推理部分用图神经网络代替。

<div align="center">
<img src="https://i.loli.net/2018/04/25/5ae08ec15eb26.png"  />
</div>

### 边的特征学习

其中的A(i,j)k表示近邻矩阵，也可理解为边的表达，相当于同时学习边的特征：

<div align="center">
<img src="https://i.loli.net/2018/04/25/5ae08f4bc886b.png"  />
</div>

其中衡量两个相邻节点之间距离信息的公式为：

<div align="center">
<img src="https://i.loli.net/2018/04/25/5ae08f6294e75.png"  />
</div>

这个公式满足距离信息的对称性(d(a,b) = d(b,a))和Identity(d(a,a) = 0).

### 初始节点的特征构建

- 已知标注

<div align="center">
<img src="https://i.loli.net/2018/04/25/5ae09b8810f01.png"  />
</div>

- 未知标注

<div align="center">
<img src="https://i.loli.net/2018/04/25/5ae09bbe7aff3.png"  />
</div>

### GNN模型：x_k经过GNN得到x_k+1 = Gc(x_k)

<div align="center">
<img src="https://i.loli.net/2018/04/25/5ae09d434b37b.png"  />
</div>
