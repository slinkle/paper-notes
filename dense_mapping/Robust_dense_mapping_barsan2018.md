# Robust Dense Mapping for Large-Scale Dynamic Environments ICRA2018

* 双目稠密重建 
* 用于大型动态环境
* 分为三类处理：静态背景，运动物体，可能会动的物体（如路边停泊的汽车）
* instance-aware 语义分割+sparse scene flow用于分类为以上三种

<div align="center">
<img src="https://i.loli.net/2018/06/05/5b15f8d6c5b94.png"  />
</div>

## 动态环境重建方法

1. 双目重构深度图并计算稀疏场景流，以及根据左目RGB进行instance-aware语义分割
2. 根据稀疏场景流计算视觉里程计VO
3. 分离color，depth和sparse flow为虚拟的多帧
4. 为每个检测到的物体根据场景流和语义分割信息估计三维运动，并和相机的自运动比较来判别这个物体是运动的还是静止的或者是未知的
5. 对每个感兴趣的刚体（运动的或者可能会动的）进行初始化或者更新它的重建模型
6. 更新静止物体的重建
7. 通过voxel garbage collection来移除一些不合理的体素
