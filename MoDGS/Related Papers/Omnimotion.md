# Tracking Everything Everywhere All at Once

```bash
python train.py --config configs/default.txt --data_dir /home/ekko/datasets/omnimotion/swing

python main_processing.py --data_dir /home/ekko/github/INN/omnimotion/data/pulling --chain

python filter_raft.py --data_dir /home/ekko/github/INN/omnimotion/data/pulling --cycle_th 3
```



## Paper

### 1. Introduction

+ 总的来说，生成既密集又长时间跨度的轨迹仍然是该领域的一个未解问题，面临着三个关键挑战：

    + 在长时间序列中保持准确的轨迹
    
    + 在遮挡情况下跟踪点
    
    + 在时空中保持一致性。

+ 在本研究中，我们提出了一种全面的视频运动估计方法，利用视频中的所有信息联合估计每个像素的完整运动轨迹。我们的方法被称为OmniMotion，它使用一种准3D表示法，其中一个标准3D体积通过一组局部标准双射映射到每一帧的局部体积。这些双射作为动态多视角几何的灵活放宽，能够建模相机和场景运动的组合。我们的表示方法保证了循环一致性，并且可以跟踪所有像素，即使在像素被遮挡的情况下（“无所不在，随处可见”）。我们通过对每个视频进行优化，联合求解整个视频的运动“全局一次性”地进行。一旦优化完成，我们的表示可以在视频中的任何连续坐标进行查询，从而得到跨越整个视频的运动轨迹。

    > [!TIP]
    >
    > "Flexible relaxation" 这里指的是对动态多视角几何的一种灵活放宽或宽松的处理方式。具体来说，**放宽**（relaxation）通常是指在某些条件下允许模型或方法更为灵活、简化或不那么严格地遵循传统的几何约束，以便适应更复杂或更广泛的情境。
    >
    > 在此文中，**灵活放宽（flexible relaxation）** 的意思是，传统的动态多视角几何可能要求严格的约束条件（如视角变化或场景运动的具体几何关系），而该方法通过使用局部标准双射（local-canonical bijections）来放松这些条件，从而使得模型能够处理更复杂的动态场景和视角变化，尤其是允许一些程度的误差或不完全的几何约束。这种“灵活放宽”使得模型能够更好地适应各种实际应用中的不确定性和复杂性。

+ 总之，我们提出了一种方法：

    + 为整个视频中的所有点生成全局一致的全长运动轨迹
    + 可以通过遮挡来跟踪点
    + 可以通过摄像机和场景运动的任意组合来处理野外视频

### 3. Overview

>
> We propose a test-time optimization approach for estimating dense and long-range motion from a video sequence. Our method takes as input a collection of frames and pairwise noisy motion estimates (e.g., optical flow fields), and uses these to solve for a complete, globally consistent motion representation for the entire video. Once optimized, our representation can be queried with any pixel in any frame to produce a smooth, accurate motion trajectory across the full video. Our method identifies when points are occluded, and even tracks points through occlusions. In the following sections, we describe our underlying representation, dubbed OmniMotion (Sec. 4), then describe our optimization process (Sec. 5) for recovering this representation from a video.

+ 提出了一种测试时优化方法，用于估计视频序列中的密集且远程的运动

+ 以一组帧和成对的噪声运动估计（例如，光流场）为输入，利用这些信息求解出整个视频的完整、全局一致的运动表示
+ 优化后，我们的表示可以通过查询任意帧中的任意像素，生成整个视频中平滑、准确的运动轨迹。我们的方法能够识别点的遮挡情况，甚至可以在遮挡情况下跟踪点

![Overview](./Omnimotion.png)

### 4. OmniMotion representation

如第1节所讨论的，传统的运动表示方法，如成对的光流，无法在物体被遮挡时跟踪其运动，并且在跨多个帧进行匹配时容易产生不一致性。为了在遮挡的情况下仍能获得准确、一致的运动轨迹，我们需要一个全局的运动表示，即一种编码场景中所有点轨迹的数据结构。这样的全局表示之一是将场景分解为一组离散的、深度分离的层[32, 81]。然而，大多数现实场景不能表示为一组固定的、有序层次：例如，考虑一个物体在三维空间中旋转的简单情况。在另一个极端是完全的三维重建，它解开了三维场景几何、相机位姿和场景运动。然而，这个问题是一个极其不适定的问题。因此，我们提出了一个问题：在没有显式的动态三维重建的情况下，我们能否准确跟踪现实世界的运动？

> We answer this question using our proposed representation, OmniMotion (illustrated in Fig. 2). OmniMotion represents the scene in a video as a canonical 3D volume that is mapped to local volumes for each frame through local-canonical bijections. The local-canonical bijections are parametrized as neural networks and capture both camera and scene motion without disentangling the two. As such, the video can be considered as a rendering of the resulting local volumes from a fixed, static camera.

我们通过提出的表示方法——OmniMotion（如图2所示）来回答这个问题。OmniMotion将视频中的场景表示为一个规范的三维体积，并通过局部规范双射将其映射到每一帧的局部体积。局部规范双射由神经网络参数化，并捕捉了相机和场景的运动，而不需要解开二者的关系。因此，可以将视频视为来自固定静态相机的渲染结果。

由于OmniMotion没有显式地解开相机和场景运动的关系，所得到的表示并不是一个物理上精确的三维场景重建。我们称之为准三维表示。通过对动态多视几何的放松，OmniMotion避开了使得动态三维重建变得困难的歧义问题。然而，我们仍然保留了在遮挡情况下进行一致且准确的长期跟踪所需的特性：首先，通过在每个局部帧和规范帧之间建立双射，OmniMotion保证了所有局部帧之间的全局循环一致的三维映射，模拟了现实世界中度量三维参考帧之间的一对一对应关系。其次，OmniMotion保留了所有场景点的信息，这些点投影到每个像素上，并保持它们的相对深度顺序，从而使得即使点暂时被遮挡，也能进行跟踪。

在接下来的章节中，我们将描述我们的准三维规范体积和三维双射，然后说明如何利用它们计算任意两帧之间的运动。