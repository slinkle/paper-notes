# Meaningful maps with object-oriented semantic mapping

Sünderhauf N, Pham T T, Latif Y, et al. Meaningful maps with object-oriented semantic mapping[C]// Ieee/rsj International Conference on Intelligent Robots and Systems. IEEE, 2017:5079-5085.

* 对于机器人来说，理解语义信息和几何信息（点线面等）一样重要。
* 本文构建的环境地图既包含语义上的物体层面的实体，又有点云或者mesh面的几何表达。
* 不仅要知道哪里有东西，还要知道那是什么东西
* 被识别为物体实体的部分和非物体部分要区分开，从而方便得知哪些3D点云是属于同一个物体上的
* 本文在对环境中的物体建模的时候，不需要任何预先已知的三维模型，因为我们要对环境中的物体进行精确的建模，而不是从模型库中寻找相似的代替，就像一把椅子，在现实环境中也或有各种各样的变体
* 构建语义地图的过程是为地图中的实体赋予语义含义的过程
* 本文要同时进行相机定位，物体检测和重构

<div align="center">
<img src="https://i.loli.net/2018/08/12/5b6fd1ab5d885.png"  />
</div>
