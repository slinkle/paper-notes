# Siamese Neural Networks for One-shot Image Recognition
 G Koch, R Zemel, and R Salakhutdinov. Siamese neural networks for one-shot image recognition. In ICML Deep Learning workshop, 2015.
 
孪生网络 **Siamese Neural Network**,衡量两个输入的相似度。当网络训练完成后，我们可以直接利用网络的超强特征实现对未知分布新样本数据的泛化识别。

训练一个网络实现对两张图片相似度的判别，当输入新图片时，从图片库中寻找最相似的作为分类。

<div align="center">
<img src="https://i.loli.net/2018/04/20/5ad99d7b21d95.png"  />
</div>

## 网络介绍

孪生网络最早是为了解决签名验证作为图像匹配问题引入的[Bromley and LeCun, 1990s]。该网络接收两个完全不同的输入并分别计算出高层次特征，然后再利用一个能量方程计算距离。这两路网络的参数是被绑定为完全相同的。这样可以保证两个十分相似的输入在映射到高维特征空间后不会相距太远，因为两路网络的映射方程是一样的。而且网络结构是对称的，这样输入图片的顺序不会影响最终结果。

<div align="center">
<img src="https://i.loli.net/2018/04/20/5ad99bd8e443b.png"  />
</div>

不同于LeCun等使用[**对比损失**](https://blog.csdn.net/autocyz/article/details/53149760) 作为相似度度量，我们直接使用带权重的L1距离结合sigmod激活函数再加上交叉熵计算损失。

<div align="center">
<img src="https://i.loli.net/2018/04/20/5ad9a0cdf0e38.png"  />
</div>

## 模型

卷积网络
