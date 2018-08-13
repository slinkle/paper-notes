# Lazy Data Association For Image Sequences Matching Under Substantial Appearance Changes

Vysotska O, Stachniss C. Lazy Data Association For Image Sequences Matching Under Substantial Appearance Changes[J]. IEEE Robotics & Automation Letters, 2017, 1(1):213-220.

* 重定位需要应对环境多样变化，比如同一地点的季节天气变化等
* a lazy data association完成不同风格的图像的匹配
* 应用一种启发式搜索方法通过一个数据关联图将当前图像在数据库中查找最相近的图像

<div align="center">
<img src="https://i.loli.net/2018/08/11/5b6ea767bd42c.png"  />
</div>

* 在线完成图像匹配
* 通过网络学习特征，用得到的数据关联图的距离衡量图片的相似度
* 通过一种启发式策略，减少图片与图片的匹配次数

## 数据关联图

* 将寻找最佳匹配图的任务变成在图中寻找最短路径的问题
* 数据关联图的每个节点代表了两张图片可能的匹配关系
* 穿越这个图的最短路径代表了图像序列的最佳匹配组合，访问节点的代价就是这两张图的相似度

