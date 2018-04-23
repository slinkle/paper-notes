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

