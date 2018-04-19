# Matching Networks for One Shot Learning

Vinyals O, Blundell C, Lillicrap T, et al. Matching Networks for One Shot Learning[J]. 2016.

用CNN实现少样本学习，受深度神经网络特征的metric learning启发。我们使用一小部分标注数据训练网络，实现对未标注物体的分类，而无需对新样本集进行fine-tune.

<div style="align: center">
<img src="https://i.loli.net/2018/04/19/5ad87828825a5.png">
</div>

## Introduction

小孩子只需要看一张长颈鹿的图片就可以形成长颈鹿的概念，而我们训练的神经网络却需要成百上千的样本来学习。one-shot learning 致力于实现从单个标注样本中形成
对该类别的概念。在我们看来，神经网络之所以学习速度慢且需要大量的样本是因为它是一个参数化的模型，该模型由大量的参数构成，需要进行大量的学习才能得到适当的
参数。当然也有非参数化的模型，比如 Nearest Neighbours,它不需要进行训练但是它取得的性能依赖于所选的度量函数（metric）。由此产生了一些非参数化的度量学习
(metric learning)的方法。我们致力于从参数化和非参数化的模型中抽取最好的特征，从而获得更好的泛化性能。

- **medeling level** Matching Networks(MN),综合了attention和memory方面的优势从而实现快速学习。
- **training procedure** 基于机器学习的原则，测试和训练的条件保持一致。
