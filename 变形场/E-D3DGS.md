# E-D3DGS (ECCV 2024)

```bash
$ python script/pre_n3v.py --videopath /home/ekko/datasets/Neural_3D_Video/cook_spinach
$ python script/downsample_point.py /home/ekko/datasets/Neural_3D_Video/cook_spinach/colmap/dense/workspace/fused.ply /home/ekko/datasets/Neural_3D_Video/cook_spinach/points3D_downsample.ply
$ python train.py -s /home/ekko/datasets/Neural_3D_Video/cook_spinach --configs arguments/dynerf/cook_spinach.py --model_path ./output --expname /home/ekko/datasets/Neural_3D_Video/cook_spinach -r 2
$ python render.py --model_path ./output --configs arguments/$DATASET/$CONFIG.py

# HDU 4090
$ CUDA_VISIBLE_DEVICES=1  python train.py -s /home/gouhao/dataset/Neural_3D_Video/cook_spinach --configs arguments/dynerf/cook_spinach.py --model_path ./output --expname /home/gouhao/dataset/Neural_3D_Video/cook_spinach -r 2
$ python render.py --model_path ./output --configs arguments/dynerf/cook_spinach.py

$ python render.py --model_path /home/ekko/datasets/Neural_3D_Video/trans --configs arguments/dynerf/cook_spinach.py --skip_train --skip_video --iteration 3000

$ CUDA_VISIBLE_DEVICES=2  python metrics.py --model_path  ./output

# Laptop 4090 HyperNeRF
python script/pre_hypernerf.py --videopath /home/ekko/datasets/HyperNeRF/vrig-3dprinter

# L-4090 Cutting
$ python train.py -s /home/ekko/datasets/EndoNeRF_PRO/cutting_tissues_twice --configs arguments/endonerf/cutting.py --model_path ./output --expname /home/ekko/datasets/EndoNeRF_PRO/cutting_tissues_twice -r 2

```

## Neural_3D_Video 数据集读取

```bash

spanish
model para 
{'sh_degree': 3, 
'source_path': '/home/ekko/datasets/Neural_3D_Video/cook_spinach', 
'model_path': './output', 
'images': 'images', 
'resolution': 2, 
'white_background': True, 
'data_device': 'cuda', 
'eval': True, 
'render_process': False, 
'loader': 'dynerf', 
'shuffle': True}

# Scene类初始化中加载数据集----------
# args.source_path = '/home/ekko/datasets/Neural_3D_Video/cook_spinach' 数据集所在地址
# args.eval = True
# duration  = 300
if loader == "dynerf": # Neural_3D_Video 数据集
            scene_info = sceneLoadTypeCallbacks["Dynerf"](args.source_path, args.source_path, args.eval, duration=300)
# 跳转至dataset_reader.py---------
# path = args.source_path
# images = args.source_path
# eval = True
# duration = 300
def readColmapSceneInfoDynerf(path, images, eval, duration=300, testonly=None)
```

```python
# 最终都是要获取一个SceneInfo类的对象
class SceneInfo(NamedTuple):
    point_cloud: BasicPointCloud
    train_cameras: list
    test_cameras: list
    video_cameras: list
    nerf_normalization: dict
    ply_path: str
    
# point_cloud--------------------------
# 从ply文件读取每个点的位置，颜色，法线，返回为BasicPointCloud对象
# 点云文件读取函数
def fetchPly(path):
    plydata = PlyData.read(path)
    vertices = plydata['vertex']
    positions = np.vstack([vertices['x'], vertices['y'], vertices['z']]).T
    colors = np.vstack([vertices['red'], vertices['green'], vertices['blue']]).T / 255.0
    normals = np.vstack([vertices['nx'], vertices['ny'], vertices['nz']]).T
    return BasicPointCloud(points=positions, colors=colors, normals=normals)
# ply文件分析
ply
format binary_little_endian 1.0
comment Created by Open3D
element vertex 93172
property double x
property double y
property double z
property double nx
property double ny
property double nz
property uchar red
property uchar green
property uchar blue
end_header
# deform3dgs endonerf cutting ini ply
ply
format binary_little_endian 1.0
element vertex 30699
property float x
property float y
property float z
property float nx
property float ny
property float nz
property uchar red
property uchar green
property uchar blue
end_header
```



## Abstract

> 由于 3D 高斯分布 (3DGS) 提供快速、高质量的新颖视图合成，因此将规范 3DGS 变形为多个帧以表示动态场景是一种自然的扩展。然而，之前的工作未能准确地重建复杂的动态场景。我们将失败归因于变形场的设计，该变形场是作为基于坐标的函数构建的。这种方法是有问题的，因为 3DGS 是以高斯为中心的多个场的混合体，而不仅仅是一个基于坐标的框架。为了解决这个问题，我们将变形定义为每高斯嵌入和时间嵌入的函数。此外，我们将变形分解为粗变形和精细变形，分别模拟慢速和快速运动。此外，我们还为每高斯嵌入引入了局部平滑正则化，以改善动态区域的细节。

+ 3DGS扩展到动态场景是一种很自然的想法
+ 3DGS是以高斯为中心的多个场的混合体，基于坐标来构建变形场是有问题的
+ 将变形定义为每高斯嵌入和时间嵌入的函数
+ 将变形分解为粗变形和精细变形，分别模拟慢速和快速运动
+ 为每高斯嵌入引入了局部平滑正则化，以改善动态区域的细节

## Introduction

> 3DGS 直接优化 3D 高斯的参数（位置、不透明度、各向异性协方差和球谐系数），并通过投影和 α 混合进行渲染。

> 由于 3DGS 具有连续体积辐射场的特征，最近的一些研究通过定义规范的 3DGS 并将其变形为单个帧（如可变形 NeRF [32] 那样）来表示动态场景。具体来说，他们将变形建模为 4D (x, y, z, t) 坐标与 MLP 或网格的函数，以预测 3D 高斯参数的变化。

> 在本文中，我们将帧处高斯变形建模为 
> **1）每高斯嵌入和时间嵌入的乘积空间的函数。我们期望这种合理的设计能够通过精确建模不同高斯的不同变形来带来质量改进。**
> **2）我们将参数的时间变化分解为粗细分量，即粗细变形。粗略变形代表场景中较大或较慢的运动，而精细变形则学习粗略变形未涵盖的快速或详细运动。**
> **3）针对每高斯嵌入的局部平滑正则化，以确保相邻高斯的变形相似。**

## Related Work

> 我们的方法使用可变形 3D 高斯，如 4DGaussians [29] 和 D3DGS [32] 所做的那样，但不需要分离特征场来获得变形解码器的输入特征。我们的方法使用分配给每个高斯的嵌入和在特定帧内共享的时间嵌入。

> 一些研究结合潜在嵌入来表示静态和动态场景的不同状态

> 我们引入每高斯潜在嵌入来编码每个高斯随时间的变化，并使用时间嵌入来表示场景每帧中的不同状态。

> 类似地，我们提出了一种局部平滑正则化，鼓励相邻高斯具有相似的嵌入，从而产生相似的变形。

## Method

### 3.2 Embedding-Based Deformation for Gaussians

> 现有的可变形高斯方法采用相同的方法来预测高斯的变形，即利用基于坐标的变形场。

> 与之前的方法不同，我们从 3DGS 的设计开始：==3D 场景表示为具有单独辐射场的高斯混合体。因此，应该为每个高斯定义变形。==

$$
\mathcal{F}_{\theta} : (\mathbf{z}_g, \mathbf{z}_t) \rightarrow (\Delta \mathbf{x}, \Delta \mathbf{r}, \Delta \mathbf{s}, \Delta \sigma, \Delta Y)
\\ \mathbf{z}_g \in \mathbb{R}^{32}, \mathbf{z}_t \in \mathbb{R}^{256}
$$

+ 这个公式表示一个参数化的函数 $\mathcal{F}_\theta$，它将输入$(z_g, z_t)$映射到输出$(\Delta \mathbf{x}, \Delta \mathbf{r}, \Delta \mathbf{s}, \Delta \sigma, \Delta Y)$。具体解释如下：
    1. **函数符号$\mathcal{F}_\theta$：** 表示一个带参数$\theta$的函数或模型。通常，这种符号用来表示深度学习模型或某种拟合函数，$\thetaθ$是模型的参数，例如神经网络的权重。

### 3.3 Coarse-Fine Deformation

> ==场景的不同部分可能有粗略和精细的运动。==例如，一只手快速搅拌平底锅（精细），而身体则缓慢地从左向右移动（粗略）。基于这种直觉，我们引入了粗细变形，它产生粗细变形的总和。

### 3.4 Local Smoothness Regularization

> 构建动态对象的相邻高斯模型往往会表现出局部相似的变形。受[17]的启发，我们为每高斯嵌入 zg 引入局部平滑正则化（图 2d），以鼓励附近高斯 i 和 j 之间的类似变形

$$
\mathcal{L}^{\text{emb\_reg}} = \frac{1}{k |\mathcal{S}|} \sum_{i \in \mathcal{S}} \sum_{j \in \text{KNN}_{i;k}} \left( w_{i,j} \| \mathbf{z}_{gi} - \mathbf{z}_{gj} \|_2 \right)
$$

