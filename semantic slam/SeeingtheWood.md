# Seeing the Wood for the Trees: Reliable Localization in Urban and Natural Environments

Tinchev G, Nobili S, Fallon M. Seeing the Wood for the Trees: Reliable Localization in Urban and Natural Environments[J]. 2018.

* Natural Segmentation and Matching(NSM),一个基于激光的在城镇和自然环境下的可靠定位算法。
* 其他方法一般很难同时适应非结构化的环境，比如森林和果园等，这样的环境中，遮挡和感知偏差使得在不同测试中的路标的重复性提取变得困难
* 在自然森林中，树木主干没有明显的辨识度，树枝之间还相互遮挡，并且完全没有平面结构
* 本文使用一种更适合与这种环境的特征提取方法用于环境识别
* 特征提取的第一步是从存在严重遮挡和交错的树叶环境点云中分割出稳定且可靠的物体点云
* 第二步，为了在当前的地图中估计传感器的位姿，我们用随机森林对提取的物体点云提取出可靠的形状描述子，并用它来生成并匹配一些可重复的有向关键位姿。

<div align="center">
<img src="https://i.loli.net/2018/09/26/5bab18e28b701.png"  />
</div>


