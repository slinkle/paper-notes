# A Unified Representation for Application of Architectural Constraints in Large-Scale Mapping -ICRA 2016

* 使用激光的大型场景三维重建
* 利用结构约束 architectural constrains
* 提供一种更自然 更统一（unified）的计算各种结构约束的公式，用于城市重建
* 垂直推扫式激光

<div align="center">
<img src="https://i.loli.net/2018/06/05/5b163251e9381.png"  />
</div>

## 简介

* 本文提出一种框架可以利用从室内或者城市环境中提取出的更高层级的特征来创建结构约束从而提高运动估计和稠密建图的精度。
* graph-formulation:图的节点是机器人的pose或者特征（路标），边是节点之间的约束。
* 场景中的元素被相机一掠而过，且只被激光扫描一次。
* 扩展Symmetries and Perturbations(SP)模型为图优化模型。
* SP模型通过为每一个几何实体/特征（点或平面）绑定参考坐标系实现统一的表示。
