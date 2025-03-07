# Instant NGP

### Paper

#### Abstract

+ 出发点：由完全连接的神经网络参数化的神经图形基元的训练和评估成本可能很高
+ 解决方案：我们通过通用的新输入编码来降低这种成本，该编码允许使用较小的网络而不牺牲质量，从而显着减少浮点和内存访问操作的数量：通过可训练特征向量的多分辨率哈希表来增强小型神经网络其值通过随机梯度下降进行优化。
+ 多分辨率网络的优势：
    + 多分辨率结构允许网络消除哈希冲突的歧义,
    + 在现代 GPU 上实现并行化的架构很简单。我们通过使用完全融合的 CUDA 内核实现整个系统来利用这种并行性，重点是最大限度地减少带宽和计算操作的浪费。  
    + 具有自适应性和高效性，和通用性
+ 效果：我们实现了几个数量级的综合加速，能够在几秒钟内训练高质量的神经图形基元，并在数十毫秒内以 1920×1080 的分辨率进行渲染。

#### INTRODUCTION

计算机图形基元基本上由参数化外观的数学函数表示。数学表示的质量和性能特征对于视觉保真度至关重要：我们希望表示在捕获高频局部细节的同时保持快速和紧凑。用作神经图形基元的多层感知器 (MLP) 所表示的函数已被证明符合这些标准

这些方法的重要共同点是将神经网络输入映射到更高维空间的编码，这是从紧凑模型中提取高近似质量的关键。这些编码中最成功的是可训练的、特定于任务的数据结构 [Liu 等人。 2020；泷川等人。 2021]承担了大部分学习任务。这使得能够使用更小、更高效的 MLP。然而，此类数据结构依赖于启发式方法和结构修改（例如修剪、分割或合并），这可能会使训练过程复杂化，将方法限制为特定任务，或者限制控制流和指针追踪成本高昂的 GPU 的性能。

我们通过多分辨率哈希编码解决了这些问题，该编码具有自适应性和高效性，且与任务无关。它仅由两个值配置 - 参数 T 的数量和所需的最高分辨率 Nmax - 经过几秒钟的训练后即可在各种任务上产生最先进的质量（图 1）。

独立于任务的适应性和效率的关键是哈希表的多分辨率层次结构：

+ 适应性：我们将级联网格映射到相应的固定大小的特征向量数组。
    + 在粗分辨率下，从网格点到数组条目存在 1:1 的映射。
    + 在高分辨率下，数组被视为哈希表，并使用空间哈希函数进行索引，其中多个网格点为每个数组条目别名。
    + 这种哈希冲突会导致冲突的训练梯度趋于平均，这意味着最大的梯度（与损失函数最相关的梯度）将占主导地位。因此，哈希表会自动对具有最重要的精细尺度细节的稀疏区域进行优先级排序。  与之前的工作不同，在训练期间的任何时候都不需要对数据结构进行结构更新。
+ 效率：我们的哈希表查找是O(1)并且不需要控制流。这很好地映射到现代 GPU，避免了树遍历中固有的执行分歧和串行指针追逐。  可以并行查询所有分辨率的哈希表。

我们在四个代表性任务中验证了我们的多分辨率哈希编码（见图 1）： 

(1) 十亿像素图像：MLP 学习从 2D 坐标到高分辨率图像的 RGB 颜色的映射。  
(2) 神经符号距离函数 (SDF)：MLP 学习从 3D 坐标到表面距离的映射。  
(3) 神经辐射缓存 (NRC)：MLP 从蒙特卡罗路径追踪器中学习给定场景的 5D 光场。  
(4) 神经辐射度和密度场 (NeRF)：MLP 从图像观察和相应的透视变换中学习给定场景的 3D 密度和 5D 光场。

在下文中，我们首先回顾先前的神经网络编码（第 2 节），然后描述我们的编码（第 3 节）及其实现（第 4 节），最后是我们的实验（第 5 节）及其讨论（第 6 节）。

#### BACKGROUND AND RELATED WORK

将机器学习模型的输入编码到高维空间的早期示例包括 one-hot 编码 [Harris and Harris 2013] 和核技巧 [Theodoridis 2008]，通过核技巧可以使复杂的数据排列线性可分。
