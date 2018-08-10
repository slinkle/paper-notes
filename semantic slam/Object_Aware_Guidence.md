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

* pre-segmentation: 增量式分割算法[Tateno2015]，分别对得到的每帧深度数据进行分割再根据估计的相机位姿增量式地将分割结果融合到一个统一的全局分割图C上,这个方法最终可以得到一些near-convex部分，比如椅子的腿和扶手。注意这里得到的部分可能不是完整的一个物体，因为有遮挡或者扫描不完整的情况。

### 模型驱动的物体识别

* 三维模型库：构建一个模型库为物体识别提供先验信息。 模型库中对一个物体有三种成分进行描述：
  * 对一个物体进行自上而下的扫描后得到的完整物体模型

  * 对其进行前述方法的分割，将分割得到的组成部分放入模型库中

  * 将分割结果相邻的两个部分成对放入模型库中

<div align="center">
<img src="https://i.loli.net/2018/08/09/5b6bf020924ae.png"  />
</div>

* 相似模型库：由于可能存在遮挡，采取部分匹配方法在模型库中寻找相似物体。选取关键点（500个），提取3D形状描述子，加上BoW方法进行部分匹配，提取出最相近的5个模型

* Objectness:两个物体匹配的相似度衡量标准：

<div align="center">
<img src="https://i.loli.net/2018/08/09/5b6bfa2a24a2c.png"  />
</div>

c是分割场景得到的模型点云，m取自M(c)，M(c)是模型库中与c最相近的模型集合。那么，d(c,m)衡量的是c相对于m的相似度，d(m,c)衡量的是c相对于m的完整度。物体性(objectness)的衡量就可以由这两个值得到：

<div align="center">
<img src="https://i.loli.net/2018/08/09/5b6bfa2da3955.png"  />
</div>

### 后分割：objectness-based

将物体性得分(objectness measurement)和识别率(recognition rate)整合到多类图分割优化算法中，实现分割和识别的同时优化。

* 公式描述：

 目标是为前面预分割得到的每个部分附上标签，这样相邻的具有相同标签的部分就可以被融合，从而得到一个较为完整的物体。首先为C中的所有部分构建一个邻接图(adjacency graph)，图的节点是预分割得到的组成部分，边代表各组成部分之间的相邻关系。基于这个邻接图，我们用以下图分割最小化公式计算后分割:
 
 
<div align="center">
<img src="https://i.loli.net/2018/08/09/5b6bff651ac0a.png"  />
</div>

由于模型库中也存放了相邻部分的组合体，所以可以更高效的进行融合。

## 物体重建

两次分割后，得到物体组合R，在当前场景表面T下。

### NBO下一个最优物体

机器人要从R中挑选出感兴趣的一个物体作为下一个要访问的对象。选择的依据是objectness score+visual saliency(显著 突出),取最大者。objectness score- O(r)衡量的是当前物体能与模型中的物体有多像，取的是模型中相似物体相似度的最大值。visual saliency score-s(r)是由当前的机器人视角决定的，由三部分组成。

<div align="center">
<img src="https://i.loli.net/2018/08/09/5b6c055dada8e.png"  />
</div>

这三部分分别代表distance,orientation,size.

### NBV 下一个最佳视角

得到最优访问物体后，机器人就向该物体移动，并根据NBV策略进行主动扫描。 

