# Shape of Motion

```bash
python run_training.py \
  --work-dir <OUTPUT_DIR> \
  --port <PORT> \
  data:iphone \
  --data.data-dir </path/to/paper-windmill/>
  
python run_training.py \
  --work-dir ./output \
  data:iphone \
  --data.data-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/backpack
  
python run_training.py --work-dir ./pulling_2025 data:custom --data.seq-name pulling --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling

python run_rendering.py \
    --work-dir ./outputs/pulling_ori

PYTHONPATH='.' python scripts/evaluate_iphone.py \
  --data_dir </path/to/paper-windmill/> \
  --result_dir <OUTPUT_DIR> \
  --seq_names paper-windmill
  
PYTHONPATH='.' python scripts/evaluate_iphone.py \
  --data_dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/backpack \
  --result_dir ./output \
  --seq_names backpack
```

```bash
# LOCAL Cutting
python process_custom.py --img-dirs /home/ekko/datasets/Ekko_2025/Shape_of_Motion/test/pulling_camera/images --gpus 0
/home/ekko/datasets/Ekko_2025/Shape_of_Motion/test/pulling_camera/images
/home/ekko/datasets/Ekko_2025/Shape_of_Motion/test/camera/images

python run_training.py --work-dir ./outputs/cutting-part-test data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_part

python run_video.py --work-dir /home/ekko/Documents/cutting data:custom  --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_4 trajectory:arc time:replay


python run_training.py --work-dir ./cutting data:custom --data.seq-name cutting --data.root-dir /hy-tmp/cutting

python run_video.py --work-dir /cutting-4 data:custom  --data.seq-name cutting --data.root-dir /hy-tmp/cutting trajectory:arc time:replay

python run_training.py --work-dir ./output/cutting-4 data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_4
/home/ekko/datasets/Ekko_2025/Shape_of_Motion/test/cutting_test-8
/home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_4
```



```bash
# 服务器
CUDA_VISIBLE_DEVICES=0 python run_training.py --work-dir ./output/cutting_119 data:custom --data.seq-name cutting --data.root-dir /home/gouhao/Github/Downloads/cutting

python run_video.py --work-dir ./output/cutting_119 data:custom  --data.seq-name cutting --data.root-dir /hy-tmp/cutting trajectory:arc time:replay
#----------------------------------------------------------------------------------
# Pulling
python run_training.py --work-dir ./outputs/pulling data:custom --data.seq-name pulling --data.root-dir /home/ekko/datasets/Shapeofmotion/Pulling_Train/pulling_ori

python run_video.py --work-dir ./outputs/pulling data:custom  --data.seq-name pulling --data.root-dir /home/ekko/datasets/Shapeofmotion/Pulling_Train/pulling_ori trajectory:arc time:replay

zip -r /media/ekko/T9/SOM/env.zip ./som

# Cutting
python run_training.py --work-dir ./outputs/cutting_full data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_part --data.is-train True

python run_val.py --work-dir ./outputs/cutting_full --model 1200 data:custom  --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_part --data.is-train False 


python run_video.py --work-dir ./calibration/cutting-part data:custom  --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_part trajectory:arc time:replay
#----------------------------------------------------------------------------------
python mask_app.py --root_dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling_soft_tissues

python process_custom.py --img-dirs /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_part/images --gpus 0

python run_training.py --work-dir ./cutting data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting

python run_training.py --work-dir ./outputs/pulling_ori data:custom --data.seq-name pulling --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling_ori

python run_training.py --work-dir ./stereo data:custom --data.seq-name stereo --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/stereo

python run_video.py --work-dir ./outputs/pulling_ori data:custom  --data.seq-name pulling --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling_ori trajectory:arc time:replay

ffmpeg -i video.mp4 -t 3 -s 640x512 -r 30 %5d.png -start_number 0 
```

```bash
# iPhone Dataset 这个可以用
python run_video.py --work-dir ./output data:iphone  --data.data-dir  /home/ekko/datasets/Ekko_2025/Shape_of_Motion/backpack trajectory:arc time:replay

python run_video.py --work-dir ./output data:iphone  --data.data-dir  /home/ekko/datasets/Ekko_2025/Shape_of_Motion/backpack trajectory:fixed time:replay


# EndoNeRF
python run_video.py --work-dir ./outdir1 data:custom  --data.seq-name pulling --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling_soft_tissues trajectory:fixed --trajectory.num-frames 240 time:replay

python run_video.py --work-dir ./outdir1 data:custom  --data.seq-name pulling --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling_soft_tissues trajectory:arc time:replay

python run_video.py --work-dir ./outdir1 data:custom  --data.seq-name pulling --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling_soft_tissues trajectory:arc time:replay

python run_video.py --work-dir ./outdir1 data:custom  --data.seq-name pulling --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling_soft_tissues trajectory:arc time:replay

python run_video.py --work-dir ./endonerf_pulling data:custom  --data.seq-name pulling --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling_soft_tissues trajectory:arc time:replay

ffmpeg -i video.mp4 -vf "fps=30" output_image/%04d.png
ffmpeg -i video.mp4 -t 3 -s 640x512 -r 30 %5d.png -start_number 0  

```



## Paper

### Abstract

由于任务的高度不适定性质，单眼动态重建是一个具有挑战性且长期存在的视觉问题。
现有方法的局限性在于它们要么依赖于模板，要么仅在准静态场景中有效，要么无法显式地对 3D 运动进行建模。在这项工作中，我们介绍了一种能够从随意捕捉的单眼视频中重建通用动态场景的方法，该场景具有明确的、全序列长的 3D 运动。

我们通过两个关键见解来解决问题的欠约束性质：

+ 首先，我们通过使用一组紧凑的 SE(3) 运动基础来表示场景运动，从而利用 3D 运动的低维结构。每个点的运动都表示为这些基础的线性组合，有助于将场景软分解为多个刚性移动的组。
+ 其次，我们利用一套全面的数据驱动先验，包括单目深度图和远程 2D 轨迹，并设计一种方法来有效整合这些噪声监控信号，从而获得动态场景的全局一致表示。

实验表明，我们的方法在远程 3D/2D 运动估计和动态场景的新颖视图合成方面均实现了最先进的性能。

> [!NOTE]
>
> 

### 1 Introduction

重建视频中持久的几何结构及其三维运动对于理解和与物理世界的交互至关重要。尽管近年来在静态三维场景建模方面取得了显著进展 [39, 61]，但从单个视频中恢复复杂动态三维场景的几何结构和运动仍然是一个未解决的挑战。一些先前的动态重建和新视图合成方法已经尝试解决这一问题。然而，大多数方法依赖于同步多视角视频 [8, 19, 19, 58, 99] 或额外的 LIDAR/深度传感器 [24, 55, 68, 91, 97]。最近的一些单目方法可以在普通动态视频上运行，但它们通常将三维场景运动建模为相邻时间帧之间的短程场景流 [20, 51, 52] 或从规范空间到视图空间的变形场 [64, 65, 108]，无法捕捉视频中持久的三维运动轨迹。

对于更通用的野外视频，长期以来的挑战在于重建问题的约束性较差。在本研究中，我们通过两个关键洞察来应对这一挑战。第一，尽管图像空间的动态可能复杂且不连续，但其底层的三维运动是由连续的简单刚体运动组成的。第二，数据驱动的先验知识虽然存在噪声，但能够提供互补的信息，这些信息可以很好地聚合为一个全局一致的三维场景几何和运动表示。

受这两个关键洞察的启发，我们将动态场景表示为一组持久的三维高斯分布，并通过一组紧凑的共享 SE(3) 运动基来表示它们在视频中的运动轨迹。与传统的场景流不同，它仅计算相邻帧之间的三维对应关系，而我们的表示方法能够在整个视频中恢复持久的三维轨迹，从而实现远距离的三维跟踪。由于我们的方法生成的三维轨迹能够捕捉每个点在三维空间和时间中的几何运动模式，我们将这种方法称为“Shape of Motion”（运动的形状），如图 1 所示。

我们展示了如何通过融合来自两个主要来源的互补线索，将我们显式的场景表示拟合到野外普通视频中：逐帧的单目深度估计以及跨帧的二维轨迹估计。我们在合成和真实世界的动态视频数据集上进行了广泛的评估，结果表明，与之前的单目动态新视图合成方法和三维跟踪基线相比，我们的方法在长距离二维和三维跟踪精度方面显著优于它们。此外，在所有现有方法中，我们还实现了最先进的新视图合成质量。

总结来说，我们的主要贡献包括：

1. 一种新的动态场景表示方法，能够实现实时新视图合成以及任意点在任意时间的全局一致三维跟踪。
2. 一个精心设计的框架，通过结合物理运动先验和数据驱动先验，在有位姿的单目视频上优化这一表示方法。

### 3 Method

> 我们的方法将动态场景的 T 视频帧序列 {It ∈ RH×W ×3}、相机内在参数 Kt ∈ R3×3 和每个输入的世界到相机外在参数 Et ∈ SE(3) 作为输入框架它。我们的目标是从这些输入中恢复整个动态场景的几何形状以及场景中每个点的全长 3D 运动轨迹。与大多数先前的动态 NeRF 方法 [21,50,52,90,100] 不同，这些方法通过体积射线投射渲染场景内容并隐式地表示固定 3D 位置的运动，我们将密集场景元素建模为一组规范的 3D 高斯，但允许它们通过完整的运动轨迹平移和旋转整个视频。我们采用基于点的显式表示，因为它同时允许 (1) 实时高保真渲染和 (2) 从任何输入时间对任何表面点进行全长 3D 跟踪。

输入: 动态场景的RGB视频帧序列$\left\{I_t \in \mathbb{R}^{H \times W \times 3}\right\}$，相机内参$\mathbf{K}_t \in \mathbb{R}^{3 \times 3}$，相机外参$\mathbf{E}_t \in \mathbb{S E}(3)$

目标: 从输入中恢复整个动态场景的几何形状，以及场景中每个点的3D运动轨迹

将密集场景元素建模为一组规范的 3D 高斯，但允许它们通过完整的运动轨迹平移和旋转整个视频。我们采用基于点的显式表示，因为它同时允许 (1) 实时高保真渲染和 (2) 从任何输入时间对任何表面点进行全长 3D 跟踪

> 从单个视频中优化动态 3D 高斯的显式表示是严重不适定的 - 在每个时间点，仅从单个视点以这些姿势观察场景中的移动主体。为了克服这种模糊性，我们提出了两个见解：
>
> 首先，我们注意到，虽然视频中投影的 2D 动态可能很复杂，但场景中底层的 3D 运动是低维的，并且由更简单的刚性运动单元组成。
>
> ‘’其次，强大的数据驱动先验，即单目深度估计和远程 2D 轨迹，提供了底层 3D 场景的互补但有噪声的信号。我们提出了一个系统，允许我们将这些噪声估计融合在一起，形成场景几何和运动的全局一致的表示。

解决单视点3DGS重建的见解: 

+ 动态运动的2D投影复杂，但是其真实的3D运动简单且可分解为刚性运动单元
+ Depth + 2D Long Trajectory提供了与3D场景互补但是有噪声的信息，三者结合可以形成场景几何和运动的全局一致表示

> 以下部分介绍我们的框架。我们将场景内容表示为一组全局一致的 3D 高斯，它们位于规范空间中（第 3.1 节）。为了恢复一致的运动轨迹，我们将 3D 高斯函数绑定到紧凑的低维运动参数化。特别是，我们用一组紧凑且低维的 SE(3) 运动基来表示每个动态场景元素的全长运动轨迹（第 3.2 节）。最后，我们将这些运动基础拟合到输入视频帧，用结构先验和数据驱动先验约束我们的优化（第 3.3 节）。我们在图 2 中展示了我们的管道示意图。

#### 3.1 Preliminaries: 3D Gaussian Splatting



#### 3.2 Dynamic Scene Representation

