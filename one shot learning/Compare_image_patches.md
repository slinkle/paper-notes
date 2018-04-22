# Learning to Compare Image Patches via Convolutional Neural Networks
Zagoruyko S, Komodakis N. Learning to compare image patches via convolutional neural networks. In CVPR 2015.

计算两张图像块的相似度，考虑到光线等各种变化。

<div align="center">
  <img src="https://i.loli.net/2018/04/23/5adcb8ef8c22c.png"  />
</div>

## 网络结构

我们设计的网络结构对输入图片的通道数不做限制，输入三通道彩色图像可以获得更好的性能。
