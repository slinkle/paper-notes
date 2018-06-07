# Too Much TV is Bad: Dense Reconstruction from Sparse Laser with Non-convex Regularisation

非凸正则方法,表面空洞填补 **surface-inpainting** -> 通过选择凸和非凸的正则项比较哪个更能捕捉场景的表面几何结构。

重写误差函数：加入正则项，几种不同的正则项R(x)：TV HUBER TGV log-TV log-TGV

<div align="center">
<img src="https://i.loli.net/2018/06/07/5b18cc821c694.png"  />
</div>

实现从稀疏激光点云到稠密点云的估计：

如图是输入的稀疏激光点云映射到图像上的表示

<div align="center">
<img src="https://i.loli.net/2018/06/07/5b18ccfddb9b4.png"  />
</div>

重建结果：

<div align="center">
<img src="https://i.loli.net/2018/06/07/5b18cd82aa03b.png"  />
</div>
