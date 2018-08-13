# Prototypical Networks for Few-shot Learning

Snell J, Swersky K, Zemel R S. Prototypical Networks for Few-shot Learning[J]. arXiv:1703.05175, 2017.

原型网络，度量学习。思想简单高效，效果也很好。

基本思想是：每个类别都存在一个聚集在某单个原型(prototype)(样本)表达周围的embedding，该类的原型是支持集在embedding空间的均值。然后，分类问题就变成在
embedding空间的最近邻问题。所以它通过学习一个度量空间(embedding space)，计算测试样本和每个类别的原型在度量空间的距离进行分类。

<div align="center">
  <img src="https://i.loli.net/2018/04/23/5adddd77a31ab.png"  />
</div>

## 模型

学习一个表征公式(embedding function):

<div align="center">
  <img src="https://i.loli.net/2018/04/23/5addde92d4398.png"  />
</div>

每个类别的原型是它对应类别的支持集在embedding space上的向量的均值：

<div align="center">
  <img src="https://i.loli.net/2018/04/23/5adddf0c129a4.png"  />
</div>

测试时使用softmax衡量分布：

<div align="center">
  <img src="https://i.loli.net/2018/04/23/5adddf890a061.png"  />
</div>

训练时最小化loss function：

<div align="center">
  <img src="https://i.loli.net/2018/04/23/5adde126f190c.png"  />
</div>

计算loss的伪代码如下：

<div align="center">
  <img src="https://i.loli.net/2018/04/23/5adde158f3af8.png"  />
</div>

## 混合密度估计

*regular Bregman divergences* 原型的学习相当于是在支持集上进行一个指数族的混合密度估计。

## 线性分类器

当采用欧式距离作为距离计算公式时，我们学习的模型就变成了一个线性分类器。

## 与匹配网络的对比
 
对于单样本学习，原型网络和匹配网络是等价的，区别在于少样本学习。少样本学习的中心是样本的均值。

对于少样本学习（而不仅仅只有一个样本）的情况，在类内进行聚类时还要考虑到一种partitioning scheme。正如[1][2]，他们需要一个额外的partitioning pahse，独立于权重更新之外的，而我们只是简单的用梯度下降进行学习。

匹配网络或许能够借鉴到原型网络上，但是会增加学习参数，事实上使用我们的方法加上一些简单的设计策略已经有可能达到与之媲美的性能。

## 可选的设计方案

- Distance Metric


  可能是因为 **squared Euclidean** 更符合Bregman divergence，实验表明它的效果要比 **cosine distance** 的效果好。

- Episode composition
 
 
  实验证明训练时的类别数比测试时多要更有利。且少量多个样本比单个样本的性能要好些。
 
## 参考文献
[1] Mensink T, Verbeek J, Perronnin F, et al. Distance-Based Image Classification: Generalizing to New Classes at Near Zero Cost[J]. IEEE Transactions on Pattern Analysis & Machine Intelligence, 2013, 35(11):2624-2637.
[2] Rippel O, Paluri M, Dollar P, et al. Metric Learning with Adaptive Density Discrimination[J]. In ICLR, 2016.
