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
python demo.py --model=models/raft-things.pth --path=data/stereomis

# LOCAL Cutting
python process_custom.py --img-dirs /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_3_7500_7580/images --gpus 0

/home/ekko/datasets/Ekko_2025/Shape_of_Motion/test/pulling_camera/images
/home/ekko/datasets/Ekko_2025/Shape_of_Motion/test/camera/images

python run_training.py --work-dir ./outputs/cutting-part-test data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_part

python run_training.py --work-dir ./outputs/stereomis/p1 data:custom --data.seq-name stereomis_p1 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P1_14940_15020

python run_video.py --work-dir /home/ekko/Documents/cutting data:custom  --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_4 trajectory:arc time:replay

python run_training.py --work-dir ./cutting data:custom --data.seq-name cutting --data.root-dir /hy-tmp/cutting

python run_video.py --work-dir /cutting-4 data:custom  --data.seq-name cutting --data.root-dir /hy-tmp/cutting trajectory:arc time:replay

python run_training.py --work-dir ./output/cutting-4 data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_4
/home/ekko/datasets/Ekko_2025/Shape_of_Motion/test/cutting_test-8
/home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_4
```

```bash
# Track
python render_tracks.py --work-dir /home/ekko/datasets/Shapeofmotion/Pulling/Track data:custom  --data.seq-name pulling --data.is-train False --data.root-dir /home/ekko/datasets/Shapeofmotion/Pulling/pulling_dataset  trajectory:arc time:replay
```

# StereoMIS

```bash
# P1
python run_training.py --work-dir ./outputs/stereomis/p1_full data:custom --data.seq-name stereomis_p1 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P1_14940_15020 --data.is-train True

python run_val_right_view.py --work-dir /home/ekko/datasets/Shapeofmotion/Cutting/cutting_40_ordinal_full --model 10000 data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Shapeofmotion/Cutting/cutting_dataset --data.is-train False

python run_compute_metrics_som.py --result_dir ./data/stereomis_p1_right_view/renders --gt_dir ./data/stereomis_p1_right_view/gts --masks_dir ./data/stereomis_p1_right_view/masks

# P2_3
python run_val.py --work-dir ./outputs/stereomis/p2_3_full --model 5000 data:custom --data.seq-name stereomis_p2_3 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_3_7500_7580 --data.is-train False

python run_val_right_view.py --work-dir ./outputs/stereomis/p2_3_full --model 5000 data:custom --data.seq-name stereomis_p2_3 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_3_7500_7580 --data.is-train False

python run_compute_metrics_som.py --result_dir ./data/stereomis_p1_right_view/renders --gt_dir ./data/stereomis_p1_right_view/gts --masks_dir ./data/stereomis_p1_right_view/masks

# P2_61
python run_val.py --work-dir ./outputs/stereomis/p2_61 --model 5000 data:custom --data.seq-name stereomis_p2_61 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_6_9740_9820 --data.is-train False

python run_val_right_view.py --work-dir ./outputs/stereomis/p2_61_full --model 5000 data:custom --data.seq-name stereomis_p2_61 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_6_9740_9820 --data.is-train False

python run_compute_metrics_som.py --result_dir ./data/stereomis_p2_6_1_right_view/renders --gt_dir ./data/stereomis_p2_6_1_right_view/gts --masks_dir ./data/stereomis_p2_6_1_right_view/masks
# P2_62
python run_val.py --work-dir ./outputs/stereomis/p2_62 --model 5000 data:custom --data.seq-name stereomis_p2_62 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_6_10050_10130 --data.is-train False

python run_val_right_view.py --work-dir ./outputs/stereomis/p2_62_full --model 5000 data:custom --data.seq-name stereomis_p2_62 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_6_10050_10130 --data.is-train False

python run_compute_metrics_som.py --result_dir ./data/stereomis_p2_6_2_right_view/renders --gt_dir ./data/stereomis_p2_6_2_right_view/gts --masks_dir ./data/stereomis_p2_6_2_right_view/masks
# P3
python run_val_right_view.py --work-dir ./outputs/stereomis/p3_full --model 6000 data:custom --data.seq-name stereomis_p3 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P3_15140_15230 --data.is-train False

python run_compute_metrics_som.py --result_dir ./data/stereomis_p3_right_view/renders --gt_dir ./data/stereomis_p3_right_view/gts --masks_dir ./data/stereomis_p3_right_view/masks


python run_val.py --work-dir ./outputs/stereomis/p2_62_full --model 5000 data:custom --data.seq-name stereomis_p2_62 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_6_10050_10130 --data.is-train False

python run_compute_metrics_som.py --result_dir ./data/stereomis_p2_6_2/renders --gt_dir ./data/stereomis_p2_6_2/gts --masks_dir ./data/stereomis_p2_6_2/masks
# P3
python run_val.py --work-dir ./outputs/stereomis/p3 --model 6000 data:custom --data.seq-name stereomis_p3 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P3_15140_15230 --data.is-train False

python run_val.py --work-dir ./outputs/stereomis/p3_full --model 6000 data:custom --data.seq-name stereomis_p3 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P3_15140_15230 --data.is-train False

python run_compute_metrics_som.py --result_dir ./data/stereomis_p3/renders --gt_dir ./data/stereomis_p3/gts --masks_dir ./data/stereomis_p3/masks

python run_training.py --work-dir ./outputs/stereomis/p2_62 data:custom --data.seq-name stereomis_p2_62 --data.root-dir /hy-tmp/stereo_P2_6_10050_10130 --data.is-train True



CUDA_VISIBLE_DEVICES=2 python run_training.py --work-dir ./outputs/stereomis/p3 data:custom --data.seq-name stereomis_p3 --data.root-dir /home/gouhao/Github/Downloads/stereo_P3_15140_15230 --data.is-train True

python run_training.py --work-dir ./outputs/stereomis/p2_61 data:custom --data.seq-name stereomis_p2_61 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_6_9740_9820 --data.is-train True

stereo_P2_6_9740_9820

python run_val.py --work-dir ./outputs/stereomis/p1_full --model 5000 data:custom --data.seq-name stereomis_p1 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P1_14940_15020 --data.is-train False

python run_val_right_view.py --work-dir ./outputs/stereomis/p1_full --model 5000 data:custom --data.seq-name stereomis_p1 --data.root-dir /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P1_14940_15020 --data.is-train False

python run_compute_metrics_som.py --result_dir ./data/stereomis_p1/renders --gt_dir ./data/stereomis_p1/gts --masks_dir ./data/stereomis_p1/masks

python run_compute_metrics_som.py --result_dir ./data/stereomis_p1_right_view/renders --gt_dir ./data/stereomis_p1_right_view/gts --masks_dir ./data/stereomis_p1_right_view/masks

```



# Cutting



```bash
# HYY
python run_training.py --work-dir ./outputs/cutting_60_ordinal data:custom --data.seq-name cutting --data.root-dir /hy-tmp/cutting --data.is-train True

python run_val.py --work-dir ./outputs/cutting_40 --model 10000 data:custom --data.seq-name cutting --data.root-dir /hy-tmp/cutting --data.is-train False

# LOCAL
python run_val.py --work-dir /home/ekko/datasets/Shapeofmotion/Cutting/cutting_30 --model 9000 data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Shapeofmotion/Cutting/cutting_dataset --data.is-train False



python run_val_right_view.py --work-dir /home/ekko/datasets/Shapeofmotion/Cutting/cutting_40_ordinal_full --model 10000 data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Shapeofmotion/Cutting/cutting_dataset --data.is-train False
```



# Pulling

```bash
# HDU
CUDA_VISIBLE_DEVICES=0 python run_training.py --work-dir ./output/pulling_60_full data:custom --data.seq-name pulling --data.root-dir /home/gouhao/Github/Downloads/pulling_ori --data.is-train True

CUDA_VISIBLE_DEVICES=0 python run_val.py --work-dir ./output/pulling_60_full --model 4000 data:custom --data.seq-name pulling --data.root-dir /home/gouhao/Github/Downloads/pulling_ori --data.is-train False
# HYY
python run_training.py --work-dir ./outputs/pulling_true data:custom --data.seq-name pulling --data.root-dir /hy-tmp/pulling --data.is-train True

python run_val.py --work-dir /root/ssh/outputs/pulling_60_ordinal --model 4000 data:custom --data.seq-name pulling --data.root-dir /hy-tmp/pulling --data.is-train False

/home/ekko/datasets/Shapeofmotion/pulling_ori_hpyer
# LOCAL
python run_val.py --work-dir /home/ekko/datasets/Shapeofmotion/Pulling/pulling_depth_full --model 4000 data:custom --data.seq-name pulling --data.root-dir /home/ekko/datasets/Shapeofmotion/Pulling/pulling_dataset --data.is-train False

python run_val_right_view.py --work-dir /home/ekko/datasets/Shapeofmotion/Pulling/pulling_depth_full --model 4000 data:custom --data.seq-name pulling --data.root-dir /home/ekko/datasets/Shapeofmotion/Pulling/pulling_dataset --data.is-train False
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
# ----------------------------------------------------------------------------------
# Cutting

python run_training.py --work-dir ./outputs/cutting_true data:custom --data.seq-name cutting --data.root-dir /hy-tmp/cutting --data.is-train True

python run_val.py --work-dir /home/ekko/datasets/Ekko_2025/cutting_true --model 5000 data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_4 --data.is-train False

python run_val.py --work-dir ./outputs/cutting_true --model 10000 data:custom  --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_4 --data.is-train False 


python run_training.py --work-dir ./outputs/cutting_full data:custom --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_part --data.is-train True

python run_training.py --work-dir ./outputs/cutting_full_ori_hyper data:custom --data.seq-name cutting --data.root-dir /hy-tmp/cutting --data.is-train True

python run_val.py --work-dir ./outputs/cutting_full --model 1200 data:custom  --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_part --data.is-train False 


python run_video.py --work-dir ./calibration/cutting-part data:custom  --data.seq-name cutting --data.root-dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting_part trajectory:arc time:replay
#----------------------------------------------------------------------------------
python mask_app.py --root_dir /home/ekko/datasets/Ekko_2025/Shape_of_Motion/pulling_soft_tissues

python process_custom.py --img-dirs /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_6_10050_10130/images --gpus 0

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

> 单目动态重建是一个具有挑战性的长期视觉问题，因其任务具有高度的病态性。现有的方法存在局限性，要么依赖模板，要么仅在准静态场景中有效，或者无法显式地建模 3D 运动。本文介绍了一种能够从随意捕捉的单目视频中重建通用动态场景的方法，具备显式的、持续整个序列的 3D 运动。我们通过两个关键的见解来解决问题的欠定性：首先，我们利用 3D 运动的低维结构，通过一组紧凑的 SE(3) 运动基表示场景运动。每个点的运动通过这些基的线性组合来表达，从而便于将场景软性分解为多个刚性运动的群体。其次，我们利用包括单目深度图和长距离 2D 跟踪在内的综合数据驱动先验，并设计了一种有效整合这些嘈杂监督信号的方法，从而获得全局一致的动态场景表示。实验结果表明，我们的方法在长时间范围内的 3D/2D 运动估计和动态场景的新视角合成方面达到了最先进的性能
>
> Keywords: Long-range 3D motion tracking · Monocular dynamic novel view synthesis · 4D Reconstruction

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

>重建视频中持久的几何结构及其三维运动对于理解和与物理世界的交互至关重要。尽管近年来在静态三维场景建模方面取得了显著进展 [39, 61]，但从单个视频中恢复复杂动态三维场景的几何结构和运动仍然是一个未解决的挑战。一些先前的动态重建和新视图合成方法已经尝试解决这一问题。然而，大多数方法依赖于同步多视角视频 [8, 19, 19, 58, 99] 或额外的 LIDAR/深度传感器 [24, 55, 68, 91, 97]。最近的一些单目方法可以在普通动态视频上运行，但它们通常将三维场景运动建模为相邻时间帧之间的短程场景流 [20, 51, 52] 或从规范空间到视图空间的变形场 [64, 65, 108]，无法捕捉视频中持久的三维运动轨迹。
>
>对于更通用的野外视频，长期以来的挑战在于重建问题的约束性较差。在本研究中，我们通过两个关键洞察来应对这一挑战。第一，尽管图像空间的动态可能复杂且不连续，但其底层的三维运动是由连续的简单刚体运动组成的。第二，数据驱动的先验知识虽然存在噪声，但能够提供互补的信息，这些信息可以很好地聚合为一个全局一致的三维场景几何和运动表示。
>
>受这两个关键洞察的启发，我们将动态场景表示为一组持久的三维高斯分布，并通过一组紧凑的共享 SE(3) 运动基来表示它们在视频中的运动轨迹。与传统的场景流不同，它仅计算相邻帧之间的三维对应关系，而我们的表示方法能够在整个视频中恢复持久的三维轨迹，从而实现远距离的三维跟踪。由于我们的方法生成的三维轨迹能够捕捉每个点在三维空间和时间中的几何运动模式，我们将这种方法称为“Shape of Motion”（运动的形状），如图 1 所示。我们展示了如何通过融合来自两个主要来源的互补线索，将我们显式的场景表示拟合到野外普通视频中：逐帧的单目深度估计以及跨帧的二维轨迹估计。我们在合成和真实世界的动态视频数据集上进行了广泛的评估，结果表明，与之前的单目动态新视图合成方法和三维跟踪基线相比，我们的方法在长距离二维和三维跟踪精度方面显著优于它们。此外，在所有现有方法中，我们还实现了最先进的新视图合成质量。总结来说，我们的主要贡献包括：
>
>1. 一种新的动态场景表示方法，能够实现实时新视图合成以及任意点在任意时间的全局一致三维跟踪。
>2. 一个精心设计的框架，通过结合物理运动先验和数据驱动先验，在有位姿的单目视频上优化这一表示方法。



### 2 Related Work

> **对应关系和跟踪** 单目 3D 长期跟踪在文献中尚未得到广泛探讨，但已有许多方法可以在 2D 图像空间中进行跟踪。确定 2D 点对应关系的典型方法依赖于光流（optical flow）。这涉及估计图像对之间的密集运动场 [4, 6, 7, 9, 15, 27, 28, 28, 31, 35–37, 57, 71, 79, 85, 86, 101]。虽然在连续帧之间效果显著，但使用光流方法进行准确的长期跟踪仍然是一个挑战。稀疏关键点匹配方法可以生成长时间轨迹 [2, 12, 53, 56, 73]，但这些方法主要用于稀疏 3D 重建。对于任意点的长时间 2D 轨迹估计，早期的研究已经探索过，这些方法依赖手工设计的先验来生成运动轨迹 [3, 72, 75, 76, 80, 92]。最近，关于该问题的兴趣有所复苏，一些工作展示了在具有挑战性的“野外”视频中出色的长期 2D 跟踪结果。这些方法采用了两种方式：一是测试时优化（test-time optimization），在这种方法中，模型将噪声较大的短程运动估计合并为一个全局表示，从而生成长期对应关系 [62, 94]；另一种是数据驱动策略 [14, 25, 38]，其中神经网络通过合成数据学习长期对应关系估计 [13, 112]。尽管这些方法能够有效跟踪视频中的任何 2D 点，但它们缺乏对底层 3D 场景几何和运动的理解。
> 场景流（Scene flow）或 3D 运动轨迹是常用的表示方式，用于建模 3D 场景的运动和点对应关系。大多数先前的工作直接从激光雷达（LIDAR）点云 [24, 55, 68, 91, 97] 或 RGBD 图像 [34, 60, 69, 84, 88, 89] 中估计场景流。在单目设置中，最近有一些研究提出通过自监督学习或测试时优化策略来估计 3D 运动 [30, 51, 52, 102–104]，但这些方法要么集中在单一物体上，要么依赖模板先验，或仅生成短程运动对应关系。相比之下，我们的方法不依赖于模板先验，能够生成长时间范围的 3D 轨迹，这使得它适合于建模包含多个移动物体的复杂场景。
>
> **动态重建与新视角合成** 我们的工作还涉及动态 3D 场景重建和新视角合成问题。在非刚性重建中，早期方法通常需要 RGBD 传感器 [5, 16, 32, 63, 113] 或强大的手工设计先验 [45, 70, 74]。近年来，研究通过整合单目深度先验 [43, 50, 59, 110, 111] 取得了在“野外”动态场景重建方面的进展。最近，基于神经辐射场（NeRF） [61] 和高斯溅射（Gaussian Splat） [40] 的方法已经达到了最先进的结果。大多数这些方法 [1, 8, 10, 19, 19, 48, 49, 81, 83, 93] 需要同时的多视角视频观测或预定义模板 [33, 47, 98] 来生成高质量的新视角输出。无需模板的单目方法通过不同类型的表示来建模动态场景，如视频深度图 [109]、时间相关的 NeRF [17, 51, 52, 64, 65, 67, 90, 100]，以及动态 3D 高斯分布 [18, 99, 107, 108]。尽管已经取得了显著进展，但正如 DyCheck [21] 所指出的，许多方法集中在相机位移 [44, 108] 或准静态场景的场景中，这些场景并不能代表现实世界中的单目视频。在本研究中，我们专注于建模由单一相机拍摄的日常视频，这是一个更具实践性且更具挑战性的设置。



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

我们通过一组全局的3D高斯分布来表示动态场景内容的外观和几何结构，这是一种显式且富有表现力的可微分场景表示，用于高效优化和渲染。我们在规范帧 $t_0 $中定义每个3D高斯分布的参数 $g_0 \equiv (\mu_0, \mathbf{R}_0, s, o, c)$，其中 $\mu_0 \in \mathbb{R}^3$、$\mathbf{R}_0 \in \mathbb{S O}(3)$是规范帧中的3D均值和方向，$s \in \mathbb{R}^3$ 是尺度，$o \in \mathbb{R} $是不透明度，$c \in \mathbb{R}^3$ 是颜色，这些属性在时间上是持久共享的。为了从一个具有世界到相机外参 $\mathbf{E}$和内参 $\mathbf{K}$的相机渲染一组3D高斯分布，3D高斯分布在图像平面中的投影通过2D高斯分布来表示，参数为 $\mu'_0 \in \mathbb{R}^2 $和 $\Sigma'_0 \in \mathbb{R}^{2 \times 2}$，通过仿射近似进行转换。
$$
\begin{equation}
\boldsymbol{\mu}_0^{\prime}(\mathbf{K}, \mathbf{E})=\mathit{\Pi} \left(\mathbf{K E} \boldsymbol{\mu}_0\right) \in \mathbb{R}^2
\end{equation}
$$

$$
\begin{equation}
\boldsymbol{\Sigma}_0^{\prime}(\mathbf{K}, \mathbf{E})=\mathbf{J}_{\mathbf{K E}} \boldsymbol{\Sigma}_0 \mathbf{J}_{\mathbf{K E}}^{\top} \in \mathbb{R}^{2 \times 2}
\end{equation}
$$

其中 $\mathit{\Pi}$是透视投影，$\mathbf{J}_{\mathbf{K}\mathbf{E}}$是在点 $\mu_0 $处，关于 $\mathbf{K}$和 $\mathbf{E}$ 的透视投影雅可比矩阵。然后，2D 高斯分布可以通过 alpha 合成有效地光栅化为 RGB 图像和深度图
$$
\begin{equation}
\hat{\mathbf{I}}(\mathbf{p})=\sum_{i \in H(\mathbf{p})} T_i \alpha_i \mathbf{c}_i, \quad \hat{\mathbf{D}}(\mathbf{p})=\sum_{i \in H(\mathbf{p})} T_i \alpha_i \mathbf{d}_i,
\end{equation}
$$
这里$\begin{equation}
\alpha_i=o_i \cdot \exp \left(-\frac{1}{2}\left(\mathbf{p}-\boldsymbol{\mu}_0^{\prime}\right)^T \boldsymbol{\Sigma}_0^{\prime}\left(\mathbf{p}-\boldsymbol{\mu}_0^{\prime}\right)\right)
\end{equation}$,$\begin{equation}
T_i=\prod_{j=1}^{i-1}\left(1-\alpha_j\right)
\end{equation}$。 $H(\mathbf{p})$是与从像素$\mathbf{p}$发射的射线相交的高斯集合。这个过程是完全可微的，并且能够直接优化 3D 高斯参数。

#### 3.2 Dynamic Scene Representation

==**场景运动参数化**== 为了建模一个动态的 3D 场景，我们跟踪 $N$个规范 3D 高斯分布，并随着时间改变它们的位置和方向，采用每帧刚性变换。具体来说，对于一个在时间点 $t$的移动 3D 高斯，其姿态参数$(\boldsymbol{\mu}_t, \mathbf{R}_t)$ 通过刚性变换从规范帧 $t_0$ 到 $t$，通过 $\mathbf{T}_{0 \to t} = \left[ \begin{matrix} \mathbf{R}_{0 \to t} \ \mathbf{t}_{0 \to t} \end{matrix} \right] \in \mathbb{S E}(3) $进行变换:
$$
\boldsymbol{\mu}_t = \mathbf{R}_{0 \to t} \mu_0 + t_{0 \to t}, \quad \mathbf{R}_t = \mathbf{R}_{0 \to t} \mathbf{R}_0
$$
与其为每个高斯独立建模 3D 运动轨迹，我们定义了一组$B \ll N$ 可学习的基轨迹 $\{ \mathbf{T}^{(b)}_{0 \to t}\}^{B}_{b=1}$，这些轨迹在所有高斯中是全局共享的。然后，在每个时间 $t$，通过每点的基系数 $\mathbf{w}^{(b)}$，将这一全局基轨迹集加权组合，计算得到变换 $\mathbf{T}_{0 \to t}$。
$$
\begin{equation}
\mathbf{T}_{0 \rightarrow t}=\sum_{b=0}^B \mathbf{w}^{(b)} \mathbf{T}_{0 \rightarrow t}^{(b)}
\end{equation}
$$
==**光栅化 3D 轨迹**== 给定这种表示方法，我们现在描述如何在任意查询帧 $I_t$ 上获取逐像素的 3D 运动轨迹。我们采用类似 Wang 等人 [94] 的方法，将 3D 高斯的运动轨迹光栅化到查询帧 $I_t$ 上。具体来说，对于在时间 $t$ 的查询相机，具有内参 $\mathbf{K}_t$ 和外参 $\mathbf{E}_t$，我们进行光栅化，以获得一个映射 $^{w}{\hat{\mathbf{X}}}_{t \to t'} \in \mathcal{R}^{H \times W \times 3}$，该映射包含了对应于目标时间 $t'$ 的每个像素的表面点的期望 3D 世界坐标
$$
\begin{equation}
{ }^{\mathrm{w}} \hat{\mathbf{X}}_{t \rightarrow t^{\prime}}(\mathbf{p})=\sum_{i \in H(\mathbf{p})} T_i \alpha_i \boldsymbol{\mu}_{i, t^{\prime}},
\end{equation}
$$
其中 $H(\mathbf{p})$ 是在查询时间 $t$ 时与像素 $\mathbf{p}$ 相交的高斯集合。对于给定像素 $\mathbf{p}$，在时间 $t'$ 的 2D 对应位置 $\hat{\mathbf{U}}_{t \to t'}(\mathbf{p}) $和对应的深度值 $\hat{\mathbf{D}}_{t \to t'}(\mathbf{p}) $可以写作：
$$
\begin{equation}
\hat{\mathbf{U}}_{t \rightarrow t^{\prime}}(\mathbf{p})=\mathit{\Pi}\left(\mathbf{K}_{t^{\prime}}{ }^{\mathrm{c}} \hat{\mathbf{X}}_{t \rightarrow t^{\prime}}(\mathbf{p})\right), \hat{\mathbf{D}}_{t \rightarrow t^{\prime}}(\mathbf{p})=\left({ }^{\mathrm{c}} \hat{\mathbf{X}}_{t \rightarrow t^{\prime}}(\mathbf{p})\right)_{[3]}
\end{equation}
$$
其中$^{c}{\hat{\mathbf{X}}}_{t \to t'}(\mathbf{p}) = \mathbf{E}_{t'}{}^{w}{\hat{\mathbf{X}}}_{t \to t'}(\mathbf{p})$,$\mathit{\Pi}$是一个透视投影操作，并且$(\cdot)_{[3]}$是一个向量的第三个元素。

#### 3.3 Optimization

我们在优化中使用现成的方法来得到以下估计结果：
1）每帧运动目标的遮罩$\{\mathbf{M}_t\}$，可通过 Track-Anything [42, 105] 在少量用户点击后轻松获得；
2）使用最先进的相对深度估计方法 Depth Anything [106] 得到的单目深度图 $\{\mathbf{D}_t\}$；
3）使用最先进的点跟踪方法 TAPIR [14] 为前景像素获得的长时序 2D 轨迹 $\{\mathbf{U}_{t \to t'}\}$。

我们通过为每帧计算全局的缩放和平移，将相对深度图与度量深度图对齐，并将其用于我们的优化，因为相对深度图通常包含更丰富的细节。随后，我们将通过对齐后的深度图进行“反投影”得到的升维 2D 轨迹视为运动目标的噪声初始 3D 轨迹观测 $\{\mathbf{X}_t\}$。对于场景中静态部分，我们使用标准的静态 3D 高斯分布建模，并通过将它们反投影到对齐后的深度图对应的 3D 空间中来初始化其 3D 位置。静态和动态的高斯分布在优化阶段被共同优化，并共同光栅化生成图像。以下部分将重点介绍动态高斯分布的优化过程。

==**初始化**== 我们首先选择可见最多 3D 轨迹的帧 $t_0$ 作为**规范帧（canonical frame）**，并将该帧中的高斯均值 $\boldsymbol{\mu}_0$ 初始化为从这批初始观测中随机采样的 $N$ 个 3D 轨迹位置。随后，我们对这些噪声 3D 轨迹 $\{\mathbf{X}_t\}$ 的**向量化速度**执行 k-means聚类，并将得到的 $B$ 个聚类用于初始化**运动基**$\{\mathbf{T}_{0 \to t}^{(b)}\}_{b=1}^B$。

具体而言，对于属于第 $b$ 个聚类的轨迹集 $\{\mathbf{X}_t\}_b$，我们在$\tau = 0, \dots, T$ 的所有时刻上，利用**加权 Procrustes 对齐**将点集 $\{\mathbf{X}_0\}_b$ 与$\{\mathbf{X}_\tau\}_b$对齐，从而初始化基转换$\mathbf{T}_{0 \to \tau}^{(b)}$。其中的加权系数由 TAPIR 的**不确定度**和**可见性得分**共同决定。接着，我们令每个高斯对应的权重 $\mathbf{w}^{(b)}$ 按与该高斯在规范帧中对应聚类中心的距离**呈指数衰减**的方式进行初始化。

最后，我们在**时间平滑性约束**下，使用 $\mathcal{l}_1$ 损失来拟合观测到的 3D 轨迹，对 $\boldsymbol{\mu}_0$、$\mathbf{w}^{(b)}$ 以及基函数集合 $\{ \mathbf{T}^{(b)}_{0 \to t}\}^{B}_{b=1}$进行优化。

==**训练**== 我们使用两组损失来监督动态高斯（dynamic Gaussians）。第一组损失包括我们的重建损失，用于匹配每帧的像素级颜色、深度和掩码输入。第二组损失则用于在时间维度上保持对应关系的一致性。具体来说，在每个训练步骤中，我们根据方程 (2)，从对应的训练相机 $(\mathbf{K}_t, \mathbf{E}_t)$ 渲染出图像 $\hat{\mathbf{I}}_t$、深度$\hat{\mathbf{D}}_t$和掩码 $\hat{\mathbf{M}}_t$。我们对这些预测逐帧地施加重建损失来进行监督。
$$
\begin{equation}
L_{\mathrm{recon}} = \|\hat{\mathbf{I}} - \mathbf{I}\|_1 
+ \lambda_{\mathrm{depth}} \|\hat{\mathbf{D}} - \mathbf{D}\|_1 
+ \lambda_{\mathrm{mask}} \|\hat{\mathbf{M}} - 1\|_1.
\end{equation}
$$
第二组损失用于监督高斯在不同帧之间的运动。具体来说，我们会对随机采样的查询时间 $t$和目标时间 $t'$ 这对时刻，额外渲染出 2D 轨迹 $\hat{\mathbf{u}}_{t \to t'} $和重投影的深度$\hat{\mathbf{D}}_{t \to t'} $。然后，我们使用“提升（lifted）的”长距离 2D 轨迹估计来监督这些渲染出的对应关系，公式如下：
$$
\begin{equation}
L_{\mathrm{track\text{-}2d}} 
= \left\| \mathbf{U}_{t \to t'} - \hat{\mathbf{U}}_{t \to t'} \right\|_1 ,
\quad\text{and}\quad
L_{\mathrm{track\text{-}depth}} 
= \left\| \hat{\mathbf{d}}_{t \to t'} - \hat{\mathbf{D}}\!\bigl(\mathbf{U}_{t \to t'}\bigr) \right\|_1.
\end{equation}
$$
最后，我们在随机采样的动态高斯与它们的 k-近邻之间施加距离保持（distance-preserving）损失。令 $\hat{\mathbf{X}}_t$ 和 $\hat{\mathbf{X}}_{t'}$ 分别表示同一个高斯在时间 $t$ 和 $t'$ 的位置，令 $\mathcal{C}_k(\hat{\mathbf{X}}_t)$ 表示 $\hat{\mathbf{X}}_t$ 的 kk-近邻集合，则我们定义：
$$
\begin{equation}
L_{\mathrm{rigidity}} 
= \bigl\| 
\mathrm{dist}\!\bigl(\hat{\mathbf{X}}_t,\; C_k(\hat{\mathbf{X}}_t)\bigr) 
- \mathrm{dist}\!\bigl(\hat{\mathbf{X}}_{t'},\; \mathcal{C}_k(\hat{\mathbf{X}}_t)\bigr) 
\bigr\|_{2}^{2},
\end{equation}
$$
其中dist$(\cdot,\cdot)$测量欧几里得距离。

==**实现细节**== 对于自然场景（in-the-wild）视频，我们通过以下步骤获取其相机参数：首先运行 UniDepth [66]，以获取相机内参和度量深度图；然后在使用 UniDepth 生成的深度图的基础上，以 RGB-D 模式运行 Droid-SLAM [87] 以获得相机位姿。该过程既高效又能提供准确的相机参数。对于在公共基准数据集上的方法评估，我们则直接使用数据集中提供的相机标注（例如来自 COLMAP [77] 或模拟环境）。我们使用 Adam 优化器 [41] 来优化模型。其中，前 1000 次迭代用于初始拟合，之后进行 500 个 epoch 的联合优化。在所有实验中，$ \mathbb{S E}(3)$ 基（bases）$B$ 的数量设为 20。场景中，动态部分初始化了 4 万个高斯，静态部分初始化了 10 万个高斯。对于动态和静态高斯，我们采用了与 3D-GS [40] 相同的自适应高斯控制策略。对于分辨率为 960×720、长度为 300 帧的视频序列，在 A100 GPU 上完成训练大约需要 2 小时。我们的渲染帧率约为 40 fps。

### 4 Experiments

我们在多种任务上对方法的表现进行了定量与定性评估，包括：长距离三维点追踪、长距离二维点追踪，以及新视角合成。我们特别针对那些在场景中存在显著运动的数据集进行评估。具体而言，iPhone 数据集 [21] 中随手拍摄的真实场景非常符合我们的目标应用场景。该数据集提供了完整的标注信息，包括同时拍摄的验证视角、激光雷达深度，以及覆盖整段视频的稀疏二维点对应关系，可用于评估我们在上述三项任务上的性能。鉴于在真实数据上获取精确三维追踪标注的难度较大，我们还使用合成的 MOVi-F Kubric 数据集 [23] 来评估我们的性能。
