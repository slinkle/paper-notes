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
* graph-formulation:图的节点是机器人的pose或者特征（路标），边是节点之间的约束，根据增加的约束重写误差方程。
* 场景中的元素被相机一掠而过，且只被激光扫描一次。
* 扩展Symmetries and Perturbations(SP)模型为图优化模型。
* SP模型通过为每一个几何实体/特征（点或平面）绑定参考坐标系实现统一的表示。

## 新的误差函数

相当于为后端优化增加了新的特征和几何约束，重新建立了误差方程，不再只是点与点之间的位姿优化Exx，还加入了平面与平面Eππ，点与平面Eπp，然后利用非线性优化方法，求得使新的误差方程最小的位姿参数。
平面相容性的判断也有助于地图的融合和回环检测的检验。尤其在室内环境，基本上都是两组正交平面构成的。在室外环境，平面的约束不是很明显。

<div align="center">
<img src="https://i.loli.net/2018/06/07/5b18c09e9d68c.png"  />
</div>

<div align="center">
<img src="https://i.loli.net/2018/06/07/5b18c0a5acd6b.png"  />
</div>
