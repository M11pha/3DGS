# 3DGS Papers

+ 论文名称链接到记录该论文的markdown文件
+ 发表时间栏链接到arXiv
+ 描述栏链接到项目主页

|论文名称 | 发表时间&会议/期刊 | 所用数据集 | 描述 | Github |
|:----------: | :-----------: |:----------: |:----------: |:----------: |
|Interactive Volume Rendering | [1989](https://users.cs.northwestern.edu/~jet/Teach/2002_1win_AdvGraphics/presentations/WestoverVolRender.pdf) |  | 3DGS起源 | - |
|Footprint Evaluation for Volume Rendering | [1990](https://dl.acm.org/doi/pdf/10.1145/97880.97919) |  | 3DGS来源 | - |
|EWA Volume Splatting | [*IEEE* VIS 2001](https://www.cs.umd.edu/~zwicker/publications/EWAVolumeSplatting-VIS01.pdf) |  | 3DGS来源 | - |
|EWA Splatting | [IEEE Transactions 2002](https://vcg.seas.harvard.edu/files/pfister/files/ewasplatting.pdf) |  |  | - |
|                                                              |                                                              |            |                                                              | |
| 3D Gaussian Splatting for Real-Time Radiance Field Rendering | [ACM Transactions on Graphics 2023.8](https://arxiv.org/abs/2308.04079) |            | [3DGS开山之作](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/) | [3DGS 14.3K](https://github.com/graphdeco-inria/gaussian-splatting) |
| 4D Gaussian Splatting for Real-Time Dynamic Scene Rendering  |    [CVPR 2024 / 2023.8](https://arxiv.org/abs/2310.08528)    |            |                                                              | [4DGS 2.2K](https://github.com/hustvl/4DGaussians) |
|  |  | | |  |
| 精确重建 |  | | |  |
| SuGaR: Surface-Aligned Gaussian Splatting for Efficient 3D Mesh Reconstruction and High-Quality Mesh Rendering |   [CVPR 2024 / 2023.11](https://arxiv.org/abs/2311.12775)    |            |                                                              | [SuGaR 2.2K](https://github.com/Anttwo/SuGaR) |
| GaussianPro: 3D Gaussian Splatting with Progressive Propagation |  | | |  |
| PGSR: Planar-based Gaussian Splatting for Efficient and High-Fidelity Surface Reconstruction |                                                              |            |                                                              |  |
|                                                              |                                                              |            |                                                              |  |

```bash
手术场景的三维（3D）重建具有促进许多下游应用的巨大潜力，包括术中导航[12]和可视化增强[13,9]。此外，高质量的动态 3D 场景模型通过以下方式展示了对手术训练的潜在好处：通过允许沉浸式观察手术场景，缩短学习曲线 [1] 和远程手术监查 [17]。

从内窥镜视频中重建高质量的可变形组织是一项重要但具有挑战性的任务，有助于外科 AR、教育和机器人学习等下游任务 [4,26,27]。早期的尝试[18,24,28,39,40]采用深度估计在内窥镜重建中取得了巨大成功，但由于两个关键问题，这些方法仍然难以产生逼真的3D重建。首先，有时具有较大运动的非刚性变形需要实际的动态场景重建，这阻碍了这些技术的适应。其次，工具遮挡发生在单视点视频中，导致在信息有限的情况下学习受影响的部分变得困难。

从内窥镜视频中重建手术场景对于机器人辅助微创手术（RAMIS）至关重要[27]。通过恢复观察到的组织的 3D 模型，此类技术有助于模拟手术环境以进行术前规划和 AR/VR 医务人员培训 [12,20]。此外，支持实时渲染的重建可以进一步扩展其在术中使用的适用性[6,17]，使外科医生能够获得完整的场景视图，并方便他们对手术器械的导航和控制，并有可能为机器人手术铺平道路。手术自动化。

内窥镜手术已成为微创手术的基石，为患者提供减少创伤和更快的恢复时间[9,16,27]。在这种情况下，内窥镜场景的准确和动态 3D 重建对于增强外科医生的空间理解和导航、促进更精确和有效的干预至关重要[13]。然而，复杂且由于视野有限、遮挡和动态组织变形等因素，内窥镜场景的受限性质对传统 3D 重建技术提出了重大挑战 [21,23,26]。

内窥镜手术是微创手术的一种重要类型,高质量的内窥镜手术场景下的动态三维重建可以促进很多下游任务的发展，比如可视化增强、术中导航、医务人员培训、术前规划等
```

