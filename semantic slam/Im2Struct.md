# Im2Struct: Recovering 3D Shape Structure from a Single RGB Image

Chengjie Niu, Jun Li and Kai Xu*, "Im2Struct: Recovering 3D Shape Structure from a Single RGB Image," CVPR 2018.

* 从单张RGB图像中恢复物体的3D形状结构信息，具体指的是由立方体代表的形状和各组成部分之间的连接关系以及对称性等

* 本文提出一种递归卷积自编码网络，包括一个对2D图像的结果解析部分和一个立方体层级的结果恢复部分

* 编码部分：由形状轮廓估计训练得到的多尺度卷积网络，从而可以尝试辨析各型各状的物体的结构

* 解码部分：融合结构解析网络产生的特征和原始图像，递归地解码出一个多层次立方体架构；由于解码网络是用来学习如何恢复物体各组成部分之间的关系，所以其对结构恢复的可信度和泛化能力可以保证。

* 这两个网络还要用轮廓掩码和立方体结构组成的成对训练数据进行协同训练，这样的训练数据是通过渲染CAD模型并进行部分分割得到的

> 是否可拓展为在复杂背景下的重构，就是先做物体分割，应该已经做了

<div align="center">
<img src="https://i.loli.net/2018/08/10/5b6d3b06142c2.png"  />
</div>

## 简介

当前很多从单张RGB图像恢复3D结构的方法都是恢复出一个三维体素模型，但是转化为体素模型就丧失了物体各组成部分之间的拓扑关系（结构关系），而结构关系对于语义的理解又是重要的。所以本文想要训练一个网络实现直接从单张图像中恢复出三维结构关系。

> 人体关节与物体组成部分能否借鉴，先识别节点
	* [人体骨架关键点识别综述](https://blog.csdn.net/sigai_csdn/article/details/80650411)
	* [人体骨架关键点检测](https://blog.csdn.net/forest_world/article/details/78157813?locationNum=2&fps=1)
	* 论文CPM:Convolution Pose Machines

> 根据单张图像恢复出三维结构从模型库中匹配，然后选择下一个视角点，将实测与估计的比较，若吻合说明预测准确，直接进行下一个物体的恢复。

> 室外深度相机失效，仅能获取RGB信息。

3D形状的表示有一下几种：

* volumetric 体素网格表示
* point clouds
* cuboid primitives
* manifold surfaces

> 如何进一步将获得的结构信息用于模型匹配，实现RGB对环境的重构，且无需多视角，与object_aware_guidence对比





