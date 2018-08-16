# Deformation-Driven Shape Correspondence via Shape Recognition

Chenyang Zhu, Renjiao Yi, Wallace Lira, Ibraheem Alhashim, Kai Xu and Hao Zhang, "Deformation-Driven Shape Correspondence via Shape Recognition," ACM Transactions on Graphics (SIGGRAPH 2017), 36(4).

* 本文提出的变形模型(deformation model)--GeoTopo transform，考虑了几何和拓扑结构的变化，比如零件拆分，重复，融合，从而发现两个物体之间的结构相似性。
* 在对两个物体进行相关性分析时，本方法最重要的是建模了一个变形能量方程，实现对几何形变的惩罚，对结构的保护，并且允许拓扑结构的变化。
* 在分析两个物体之间的相似性时，我们对其中一个物体施加最小能量变化，使其形状变化为与另一个最相似的形状。该形变是拓扑结构可变，几何结构保护的。
* 我们用结构图structual graph来代表物体的3D形状，其节点是物体部分的curve和sheet，连接物体各部分之间的curve，sheet被视为structual rods，一种类似于弹簧的结构。从几何结构和拓扑中建模能量方程时，考虑的更多是物体各部分之间的相对测量值而非绝对值。

<div align="center">
<img src="https://i.loli.net/2018/08/15/5b7414c3b662e.png"  />
</div>

## 文章思路

本文的算法输入是两个待计算相关性的物体（a pair of 3D shapes）。而且输入的3D shape已经旋转至朝上，并且做了相关部分的分割。算法输出的是一个分段连续的part-to-part的映射。形状的分割是人工手动完成的，每个3D形状被分割为一些1D线条或者2D架子，如图所示，他们之间的连接关系和对称关系等会用结构图来表示。

<div align="center">
<img src="https://i.loli.net/2018/08/15/5b741647b677d.png"  />
</div>

之前的方法的结构图中的节点是物体的独立关节（零件部分），本文的方法中将节点改为代表一种对称关系，即代表了一组零件，可能是a single self-reflectional,rotational,translational symmetry。

在两个物体之间衡量相关性时，可能是一个零件对应于一个零件，也有一对多的情况。这两种情况被我们结合为一种，公式化为全局最优的NP求解问题。

* 结构保护

零件之间的对称性，相对位置关系和连接性。其中，对称性有三种：reflectional,rotational,translational，相对位置关系关心的是零件A在B的上面，前面还是左边，而不是在上面多远等。连接性代表相邻零件之间的连接关系。这些关系都是要维护的，不能改变的。














