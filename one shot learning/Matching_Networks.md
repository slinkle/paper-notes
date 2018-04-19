# Matching Networks for One Shot Learning

Vinyals O, Blundell C, Lillicrap T, et al. Matching Networks for One Shot Learning[J]. 2016.

用CNN实现少样本学习，受深度神经网络特征的metric learning启发。我们使用一小部分标注数据训练网络，实现对未标注物体的分类，而无需对新样本集进行fine-tune.

<div align="center">
  <img src="https://i.loli.net/2018/04/19/5ad87828825a5.png" />
</div>

## Introduction

小孩子只需要看一张长颈鹿的图片就可以形成长颈鹿的概念，而我们训练的神经网络却需要成百上千的样本来学习。one-shot learning 致力于实现从单个标注样本中形成
对该类别的概念。在我们看来，神经网络之所以学习速度慢且需要大量的样本是因为它是一个参数化的模型，该模型由大量的参数构成，需要进行大量的学习才能得到适当的
参数。当然也有非参数化的模型，比如 Nearest Neighbours,它不需要进行训练但是它取得的性能依赖于所选的度量函数（metric）。由此产生了一些非参数化的度量学习
(metric learning)的方法。我们致力于从参数化和非参数化的模型中抽取最好的特征，从而获得更好的泛化性能。

- **medeling level**: Matching Networks(MN),综合了attention和memory方面的优势从而实现快速学习。
- **training procedure**: 基于机器学习的原则，测试和训练的条件保持一致。

## model architecture

为神经网络加入记忆机制 P(B|A) A和B可以是sequence，也可以是sets（更符合我们的需求）。 set-to-set

预测公式如下：非常类似于 Nearest Neighbours 的公式

![捕获.PNG](https://i.loli.net/2018/04/19/5ad8833283e57.png) 

其中x_i和y_i是训练样本集S的样本和对应标注，a是感知机模型。可以看出新物体的类别预测是样本集中标注的线性组合。

1. 我们可以这样看，把a看成一个感知机，y_i是绑定在x_i上的一些记忆，当输入新数据时，从记忆中找出最相似的进行标注。
2. 该公式是一个非参数化的形式，当训练集增大时，对应的记忆量也增大，所以能更好的适应新的输入集。

一个端到端的可微分最近邻

其中的感知机模型如下：类似于余弦距离的softmax

![捕获.PNG](https://i.loli.net/2018/04/19/5ad88b3f81caa.png)

- 1. g 基于 bidirectional LSTM
- 2. f 基于set2set LSTM

## 训练策略

将数据分成支持集S和batch B，学习支持集使得对batch进行分类得到的误差最小。从整体数据中不断采样得到S和B。




