# 

使用全卷积网络（FCN）模型进行切片到体积重建（SVR）可以绕过依赖手工设计的采集特定重建流程以及数值优化过程。与其他基于学习的方法通常将SVR表述为预测3D空间中切片的绝对坐标不同【28–32】，我们将SVR建模为将某个未观测到的3D体积与一组观测到的2D切片进行配准的过程。我们训练一个FCN模型，仅以切片作为输入，预测切片与3D体积之间的运动关系，并在配准过程中生成3D体积作为副产品。从概念上讲，这与单目深度估计问题【40–43】类似，在单目深度估计中，目标是预测与单张2D图像相关的视差（沿极线的运动），以确定底层3D场景的深度。

```bash
$ python crl.py
```

