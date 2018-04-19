# Siamese Neural Networks for One-shot Image Recognition
 G Koch, R Zemel, and R Salakhutdinov. Siamese neural networks for one-shot image recognition. In ICML Deep Learning workshop, 2015.
 
孪生网络 Siamese Neural Network,衡量两个输入的相似度。当网络训练完成后，我们可以直接利用网络的超强特征实现对未知分布新样本数据的泛化识别。

训练一个网络实现对两张图片相似度的判别，当输入新图片时，从图片库中寻找最相似的作为分类。
