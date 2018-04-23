# Learning to Compare Image Patches via Convolutional Neural Networks
Zagoruyko S, Komodakis N. Learning to compare image patches via convolutional neural networks. In CVPR 2015.

计算两张图像块的相似度，考虑到光线等各种变化。

之所以阅读这篇文章，是想与孪生网络进行对比。同年发表的。


<div align="center">
  <img src="https://i.loli.net/2018/04/23/5adcb8ef8c22c.png"  />
</div>

## 网络结构

我们设计的网络结构对输入图片的通道数不做限制，输入三通道彩色图像可以获得更好的性能。

该文主要是设计了大概三类网络模型及其变种进行相似度评分的实验，比较性能。

<div align="center">
  <img src="https://i.loli.net/2018/04/23/5add8ce63d1ec.png"  />
</div>

### 1. 2-channel

将两张输入图片看成是两通道的一张图片，共同输入一路网络进行相同的处理，联合学习(***jointly***)

### 2. siamese-based

两张图片分别输入两路结构相同的网络进行特征提取，在顶层决策网络根据某种规则（如*l1*或*l2*距离）进行相似度计算
其中孪生网络siamese network 的两路分支网络不仅结构相同且共享相同参数，而pseudo-siamese网络的参数不共享，各自训练

### 3. central-surround

对64x64大小的图片进行两次操作，一次是截取中间32x32大小的patch构成central patch,一次是将原图以2为步长进行降采样，得到surround patch。这样来讲，图片中间的信息被利用了两次，使得中间图像的信息对最终结果造成的影响比较大。

## 训练

目标函数：其中y_i={-1，1},-1表示不匹配图像对，1表示匹配，o_i(net)表示第i个样本的网络输出结果

<div align="center">
  <img src="https://i.loli.net/2018/04/23/5add8fd40b95d.png"  />
</div>

## 实验及结果

### 局部图像块的实验

综合实验结果来看，2ch-2stream获得最好的性能，证明了联合训练和融合多尺度信息的优势。



