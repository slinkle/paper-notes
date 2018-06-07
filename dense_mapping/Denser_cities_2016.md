# DENSER Cities:A System for Dense Efficient Reconstructions of Cities

主要是将regularizer应用到城市环境的三维重建中，使重建结果平滑，精度高，精简却精度高。

Regularizer + HVG(hash voxel garbage)

在深度图的估计和融合过程中我们都加入了对凸优化的限制和正则项。

<div align="center">
<img src="https://i.loli.net/2018/06/07/5b18c3a12a831.png"  />
</div>

## 地图构建和融合中的正则项

重写误差方程，加入正则项，并求梯度和散度。这是一个凸能量最小化问题，可以用Primal-Dual方法求解。

<div align="center">
<img src="https://i.loli.net/2018/06/07/5b18c68f18f8c.png"  />
</div>

其中正则项一般指TV正则（Total Variation）。

## 深度图估计中的正则项

用最小化能量方程的方法实现对双目的深度估计。此时加入的正则项是TGV(Total Global Variation).
