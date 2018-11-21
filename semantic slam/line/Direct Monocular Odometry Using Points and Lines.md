# Direct Monocular Odometry Using Points and Lines
从帧到关键帧的单目视觉里程计算法
* 为关键帧中梯度值高的像素（edges）维持一个semi-depth地图，当有新的帧进入时，按如下三个步骤处理：

1. 检测直线段并与关键帧中的edge进行匹配

2. 相机位姿的跟踪：最小化一个像素的光度误差和属于edge的像素的几何重投影误差

3. 更新depth map

检测到的边缘可用于加速双目对边缘像素的搜索，也可以通过一个高效的3D直线正则化提高重构的精度

> 理解一下直线的正则化

<div align="center">
<img src="https://i.loli.net/2018/10/22/5bcdd34d01cec.png"  />
</div>

