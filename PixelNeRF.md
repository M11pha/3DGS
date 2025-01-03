# Pixel-NeRF

## Introduction

我们研究从一组稀疏的输入视图合成场景的新颖视图的问题。虽然 NeRF 可以渲染逼真的新颖视图，但它通常是不切实际的，因为它需要大量的姿势图像和冗长的场景优化。

在本文中，我们通过提出 PixelNeRF 来解决这些缺点，这是一种学习框架，能够以前馈方式从一张或多张图像中预测 NeRF。与不使用任何图像特征的原始 NeRF 网络不同，pixelNeRF 将与每个像素对齐的空间图像特征作为输入。这种图像调节允许框架在一组多视图图像上进行训练，其中它可以学习场景先验，以从一个或几个输入视图执行视图合成。相比之下，NeRF 无法泛化，当可用输入图像很少时，表现很差，如图 1 所示

具体来说，我们通过首先从输入图像计算完全卷积图像特征网格来对输入图像进行 NeRF 条件处理。然后，对于视图坐标系中感兴趣的每个查询空间点x和观察方向d，我们通过投影和双线性插值来采样相应的图像特征。查询规范与图像特征一起发送到输出密度和颜色的 NeRF 网络，其中空间图像特征作为残差馈送到每一层。当多个图像可用时，输入首先被编码为每个相机坐标系中的潜在表示，然后在预测颜色和密度之前将其汇集到中间层中。该模型通过地面实况图像和使用传统体积渲染技术渲染的视图之间的重建损失进行监督。该框架如图 2 所示。

PixelNeRF 对于少视图新颖视图合成具有许多理想的特性。首先，pixelNeRF 可以在多视图图像数据集上进行训练，无需额外的监督，例如地面实况 3D 形状或对象掩模。其次，pixelNeRF 预测输入图像的相机坐标系中的 NeRF 表示，而不是规范坐标系。这不仅对于泛化到未见过的场景和对象类别[42, 38]来说是不可或缺的，而且对于灵活性来说也是不可或缺的，因为在具有多个对象的场景或真实场景中不存在明确的规范坐标系。第三，它是完全卷积的，允许它保留图像和输出 3D 表示之间的空间对齐。最后，pixelNeRF 可以在测试时合并可变数量的姿势输入视图，而不需要任何测试时优化。

我们对合成图像和真实图像数据集进行了一系列广泛的实验，以评估我们框架的有效性，超越了通常的 ShapeNet 实验集，以证明其灵活性。我们的实验表明，pixelNeRF 可以针对特定类别和类别不可知的设置从单个图像输入生成新颖的视图，即使是在看不见的对象类别的情况下也是如此。此外，我们还使用 ShapeNet 的新多对象基准（其中 PixelNeRF 优于先前的方法）以及真实汽车图像上的模拟到真实传输演示来测试我们框架的灵活性。最后，我们使用 DTU 数据集 [14] 在真实图像上测试 PixelNeRF 的功能，尽管在不到 100 个场景上进行了训练，但它可以从三个姿势输入视图生成真实场景的合理新颖视图

## Image-conditioned NeRF

为了克服 NeRF 表示无法在场景之间共享知识的问题，我们提出了一种架构来根据空间图像特征来调节 NeRF。我们的模型由两个组件组成：一个全卷积图像编码器 E，它将输入图像编码为像素对齐的特征网格；以及一个 NeRF 网络 f，在给定空间位置及其相应的编码特征的情况下，输出颜色和密度。出于第 2 节中讨论的原因，我们选择在输入视图的相机空间而不是规范空间中对空间查询进行建模。我们在未见过的对象类别（第 5.2 节）和复杂的未见场景（第 5.2 节）的实验中验证了这种设计选择。 5.3）。该模型使用第 3 节中描述的体积渲染方法和损失进行训练。



我们现在描述从一幅输入图像渲染新颖视图的方法。

+ 坐标系为输入图像的视图空间，并在该坐标系中指定位置和相机光线。给定场景的输入图像 I，首先提取特征量 W = E(I)。
+ 对于相机射线 x 上的点，我们通过将 x 投影到图像平面上的图像坐标 π(x) 来检索相应的图像特征，然后在像素特征之间进行双线性插值以提取特征向量 W(π(x))
+ 然后将图像特征连同位置和视图方向（均在输入视图坐标系中）一起传递到 NeRF 网络中，图像特征作为残差合并到每一层；
+ 在少镜头视图合成任务中，查询视图方向是确定 NeRF 网络中特定图像特征重要性的有用信号。如果查询视图方向与输入视图方向相似，则模型可以更直接地依赖输入；如果不相似，模型必须利用学到的先验知识。
+ 此外，在多视图情况下，视图方向可以充当不同视图的相关性和定位的信号。因此，在 NeRF 网络的开头输入视图方向



```bash
python eval/gen_video.py  -n dtu --gpu_id=0 --split val -P '22 25 28'  -D data/rs_dtu_4 -S 1 --scale 0.25

python train/train.py -n dtu_exp -c conf/exp/dtu.conf -D data/rs_dtu_4 -V 3 --gpu_id=0 --resume
```

