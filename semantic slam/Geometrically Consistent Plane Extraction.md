# Geometrically consistent plane extraction for dense indoor 3D maps segmentation

Pham T T, Eich M, Reid I, et al. Geometrically consistent plane extraction for dense indoor 3D maps segmentation[C]// Ieee/rsj International Conference on Intelligent Robots and Systems. IEEE, 2016:4199-4204.

* 仅用几何信息的非监督3D点云地图分割算法：提取平面--墙和地面，分割物体--桌子椅子等

* 一种分割3D地图为物体的方法是CRF，这个方法需要大量的标注数据用于分类。而且，CRF推理阶段还需要很大的计算量。
* 本文提出一种非监督的几何方法可以将3D地图分割为一个一个的物体并给出场景语义结构信息
* 我们将输入的点云近似为一些表层碎片的邻接图，连接这些碎片的边被标注为是否属于同一物体，在对这个图进行聚类（graph clustering）时就可以完成物体的分割
* 在对边进行分类时，全局平面和局部surface convexities都被考虑在内
* 另外，我们提出了一种鲁棒的提取全局平面的算法，用于提取场景中的平面
* 并且保证提取的平面之间是正交或者平行的关系，更符合室内环境的构造
