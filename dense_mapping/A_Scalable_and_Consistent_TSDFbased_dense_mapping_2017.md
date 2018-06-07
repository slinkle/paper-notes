# A Scalable and Consistent TSDF-based Dense Mapping Approach

得到一个连续的压缩的，地图大小不会随着轨迹边长而大幅增长的TSDF稠密地图。

* map consistency
* scalability to limit map growth

通过概率计算得到享有冗余视角的subvolumes，然后进行融合。

<div align="center">
<img src="https://i.loli.net/2018/06/07/5b18d174da1f1.png"  />
</div>

## 连续性

我们假设每个子体素内部是连续的，所以为保持地图的连续性我们需要今早且经常划分子体素。产生新的子体素的条件有两个：

1. 该子体素的关键帧的数目累积到一个极大值
2. 从稀疏地图中可以看出显著的跳跃变化

我们为提升voxblox的地图构建的时间性能，将其改造为多线程的快速构建方法：
（以下看不懂）：

大体思路是如果这个地区已经被其他射线扫描且构建过就直接放弃这条射线的信息。主要包括两种情况：

1. 计算starting points的密度：
