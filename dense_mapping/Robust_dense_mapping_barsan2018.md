# Robust Dense Mapping for Large-Scale Dynamic Environments ICRA2018

* 双目稠密重建 
* 用于大型动态环境
* 分为三类处理：静态背景，运动物体（不包括行人），可能会动的物体（如路边停泊的汽车）
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

### 双目恢复深度

两种方法：ELAS和DispNet
ELAS方法重构的深度图边缘锋利但不完整，Dispnet的深度图稠密鲁棒但是边界部分不锋利。

### 物体分割和2D跟踪

从单张图片分割出运动和可能会动的物体实例。方法:Multi-task Network Cascades.物体检测是每帧单独完成的。
对于2D跟踪，简单的采用IOU进行判断，如果当前帧检测到的物体与已经存在的物体的IOU大于某一阈值则继续跟踪，否则初始化一个新的跟踪。行人是被去除的。

### 稀疏场景流和视觉里程计

libviso2:左目和右目的当前帧和上一帧进行3D点对的匹配，用来计算场景流，和视觉里程计，估计物体的3D运动和相机的6D位姿。

### 3D物体跟踪

假设物体静止，用分割的物体和对应部分的场景流来估计一个虚拟相机的运动。如果估计成功，那么物体运动的估计应该是该相机运动的逆。如果估计出的虚拟相机的运动和双目相机的自运动一样，那么物体就是真实静止的。这个虚拟相机的运动估计和之前相机自运动的估计一样，也是用libviso2实现。

### 静止地图构建以及单物体重构

本文用InifiniTAM进行体素融合。利用相机的自运动和语义分割的结果对静止背景的彩色和深度图进行地图构建。对于运动的和可能会动的物体再单独构建。每个物体都是一个单独的体素模型，其坐标系是看到该物体的第一帧相机的坐标系。根据分割结果可以得到一个只含有该特定物体的虚拟帧，以此和估计的3D运动作为物体重构的输入。

### 地图融合

对于大型室外场景的双目重构来讲，噪声不可忽略。去除最大权重为0的体素。且只保存一段时间内的可见体素。这只针对静止的地图。汽车还是完整融合。









