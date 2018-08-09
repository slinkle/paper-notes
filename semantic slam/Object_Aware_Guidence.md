# Object-Aware Guidance for Autonomous Scene Reconstruction

Ligang Liu, Xi Xia, Han Sun, Hui Huang and Kai Xu*, "Object-Aware Guidance for Autonomous Scene Reconstruction," ACM Transactions on Graphics (SIGGRAPH 2018), 37(4)

* 仅规划一条路径实现未知环境的自动扫描和三维重建
* 从对物体的分析层面来引导机器人对环境的扫描
* 两个概念：Next Best Object(NBO)(用于全局探索) 和 Next Best View(NBV)(用于局部扫描)

具体流程如下：

首先，机器人将视野内的物体进行分割和语义识别，得到感兴趣的物体并以此作为NBO进行进一步的扫描和重建。扫描时的视角由NBV策略所得，直到该物体被完整的重建出来，我们就将其用数据库里最相近的3D模型代替。该算法持续迭代直到环境中的所有物体都被识别和重建。

<div align="center">
<img src="https://i.loli.net/2018/08/09/5b6bad8439ebb.png"  />
</div>

## 物体分割

### 预分割

* SLAM框架：采用的是Whelan2015的 GPU版 dense RGB-D SLAM 框架，surfel-based融合方法，全局闭环检测

* pre-segmentation: 增量式分割算法[Tateno2015]，分别对得到的每帧深度数据进行分割再根据估计的相机位姿增量式地将分割结果融合到一个统一的全局分割图上,这个方法最终可以得到一些near-convex部分，比如椅子的腿和扶手。注意这里得到的部分可能不是完整的一个物体，因为有遮挡或者扫描不完整的情况。

### 模型驱动的物体识别

* 三维模型库：构建一个模型库为物体识别提供先验信息。 模型库中对一个物体有三种成分进行描述：
  * 对一个物体进行自上而下的扫描后得到的完整物体模型

  * 对其进行前述方法的分割，将分割得到的组成部分放入模型库中

  * 将分割结果相邻的两个部分成对放入模型库中

<div align="center">
<img src="https://i.loli.net/2018/08/09/5b6bf020924ae.png"  />
</div>