# Experiment

## 3.1 Experiment Setting

==**Datasets.**==

我们在两个数据集上对方法的有效性进行了定量与定性评估：1）EndoNeRF数据集是一个立体内窥镜视频数据集，包含六个立体手术片段的视频，每个片段包含工具遮挡和一定的组织变形。2）StereoMIS数据集是一个立体内窥镜视频数据集，包含11个立体手术序列。具体来说，我们使用两个可获得的EndoNeRF场景和5个从SrereoMIS数据集中精心选择的切片。这些场景片段涵盖了呼吸，工具运动和不同重建难度的组织变形。

==**Evaluation setting.**== 

我们使用两种评估策略进行实验：1）主视角抽帧对比。遵循以前方法的策略，我们将每个视频帧序列按7:1的比例划分为训练集和测试集。2）新视角生成对比。我们以左视图（主视图）作为训练集，右视图作为测试集，来对方法进行更为全面的性能评估。

==**Implementation Details.**==



## 3.2 Comparison with State-of-the-art Methods



##  3.3 Quantitative Evaluation of Key Components