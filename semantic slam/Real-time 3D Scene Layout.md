# Real-time 3D scene layout from a single image using Convolutional Neural Networks

Yang S, Maturana D, Scherer S. Real-time 3D scene layout from a single image using Convolutional Neural Networks[C]// IEEE International Conference on Robotics and Automation. IEEE, 2016:2183-2189.

* 实时从单张图像中构建室内走廊环境的三维布局
* 现在的很多基于单张图像的重构方法大都会做Manhattan-World的假设，不符合这个模式的就进行拆分（break down）
* 本文提出结合机器学习和几何建模来从单张图像中重构环境的简化三维模型

流程如下：

  * 先用一个监督CNN对场景进行稠密但粗糙的几何分类(geometric class labeling)
  * 随即用一个全连接的条件随机场(CRF)进行细化
  * 最后提取墙和地面的边界线条结合几何约束 pop up 出一个3D model
  
<div align="center">
<img src="https://i.loli.net/2018/08/12/5b6f9a96d9943.png"  />
</div>

## 简介

我们希望机器人也能像人一样，通过单张图片就能判断出哪里是墙，哪里是路，包括在特征不丰富或者光线较弱甚至有遮挡的环境中。

本文的方法包含两部分，一个是用学习的方法检测地面和墙面，一个是几何建模得到对于场景的简化三维平面模型。

  * 学习部分，用CNN+CRF对图像的每个像素预测几何布局分类标签
  * 结合几何约束计算墙面和地面的夹角(relative orientations)并整合到3D模型中
