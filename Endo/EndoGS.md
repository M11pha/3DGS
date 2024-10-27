# EndoGS

## 实验记录

|      Time/Device       |      数据集      |     PSNR      |     SSIM     |    LPIPS     |             备注             | Train Time | GPU Memory | 迭代次数 |
| :--------------------: | :--------------: | :-----------: | :----------: | :----------: | :--------------------------: | :--------: | :--------: | :------: |
|         Paper          |     EndoNerf     | 37.935(0.088) | 0.966(0.003) | 0.066(0.030) |                              |            |            |  3K+60K  |
| 2024.10.25/4090 Laptop | EndoNerf-Cutting |    34.623     |    0.947     |    0.0486    |                              |            |            |  3K+60K  |
|  24.10.27/4090 Server  | EndoNerf-Cutting |    34.983     |    0.950     |    0.048     |                              |     1h     |    Full    |  3K+60K  |
|  24.10.27/4090 Server  | EndoNerf-Pulling |    36.249     |    0.953     |    0.0699    | colmap 3.8 windows with cuda |  40 mins   |    Full    |  3K+60K  |



## 其他论文对该工作的评价

+ [ManiGaussian](https://arxiv.org/pdf/2403.08321) 第四页 引用号82

    > For deformation modeling, time-variant Gaussian radiance fields [1, 37, 44, 66, 69, 71, 72] were reconstructed from videos instead of images, which are widely applied in applications such as surgical scene reconstruction [42, 82]. Although these approaches have achieved high-quality reconstruction from entire videos like interpolation, **extrapolation to future states conditioned on previous states and actions is unexplored, which holds significance for scene-level dynamics modeling for interactive agents**. In this paper, we formulate a dynamic Gaussian Splatting framework to model the scene dynamics of object interactions, which enhances the physical reasoning for agents to complete a wide range of robotic manipulation tasks.
    >
    > 尽管这些方法已经实现了从整个视频（如插值）进行高质量重建，**但尚未探索基于先前状态和动作推断未来状态的方法，这对于交互式代理的场景级动态建模具有重要意义**。在本文中，我们制定了一个动态高斯 Splatting 框架来模拟对象交互的场景动态，这增强了代理完成各种机器人操作任务的物理推理能力 

+ [Tracking and mapping in medical computer vision: A review](https://www.sciencedirect.com/science/article/pii/S1361841524000562)  第22页 最后一个引用

    > Bringing these works into endoscopy, Zhu et al. (2024) extend 4D Gaussian Splatting (Wu et al., 2023). They adjust it by adding depth guidance for training and demonstrate high performance. They mention that there is still possibility for artifacts and ambiguities in novel views, and recommend surface-alignment (Guédon and Lepetit, 2023) for future work. Liu et al. (2024) is another work to use 4D Gaussian splatting. Chen and Wang (2024) do similarly with image inpainting and depth regularization. Huang et al. (2024) also use 4D Gaussian splatting, and train efficiently, using Depth-Anything (Yang et al., 2024) for depth supervision via a ranked loss scheme. That said, inference can still be slow, and these require manually masking instruments.
    >
    > 将这些作品带入内窥镜检查，Zhu 等人 (2024)**(EndoGS)** 扩展了 4D 高斯分层 (Wu 等人，2023)。他们通过添加深度指导进行调整，以进行训练并展示高性能。他们提到，在新视图中仍然存在伪影和歧义的可能性，并建议在未来的工作中使用表面对齐 (Guédon and Lepetit, 2023)。刘等人 (2024)**(EndoGaussian)** 是另一项使用 4D 高斯分层的工作。陈和王 (2024) 对图像修复和深度正则化做了类似的事情。黄等人 (2024) **(Endo-4DGS)**也使用 4D 高斯分层，并通过排名损失方案使用 Depth-Anything (Yang 等人，2024) 进行深度监督，从而实现高效训练。**话虽如此，推理仍然可能很慢，而且这些需要手动屏蔽仪器**

## 预处理方法

+ 本地复现时，用colmap 3.8 windows with cuda生成初始点云

## 指标计算方法

+ 全部的渲染图片

+ PSNR : 非工具处
+ SSIM : 全局
+ LPIPS: 全局

> We evaluate our proposed method on the dataset from [29]: typical robotic surgery videos from 6 cases of DaVinci robotic data. The datasets are designed to capture challenging surgical scenes with non-rigid deformation and tool occlusion. We use standard image quality metrics, including PSNR, SSIM, and LPIPS. Since in evaluation the groundtruth pixels for unseen areas are missing, the tool masks are used to exclude unseen parts for computation and unlike [29, 32, 33], we do not count those pixels in PSNR. We also report the frame per second (FPS) to compare the rendering speed of the methods. Besides, while former works [29, 32, 33] adopt the different tool mask configurations in training and evaluation or compare methods under different configurations, we argue to train and evaluate in the same tool mask configurations to prevent meaningless pixels comparison, and compare methods the same tool occlusion masks.
>
> 我们在[29]的数据集上评估了我们提出的方法：来自 6 个达芬奇机器人数据的典型机器人手术视频。该数据集旨在捕获具有非刚性变形和工具遮挡的具有挑战性的手术场景。我们使用标准图像质量指标，包括 PSNR、SSIM 和 LPIPS。由于在评估中未见区域的真实像素丢失，因此工具掩模用于排除计算中未见的部分，并且与[29,32,33]不同，我们不将这些像素计入 PSNR。我们还报告了每秒帧数 (FPS)，以比较这些方法的渲染速度。此外，虽然以前的工作[29,32,33]在训练和评估中采用不同的工具掩模配置或在不同配置下比较方法，但我们主张在相同的工具掩模配置中进行训练和评估以防止无意义的像素比较，并比较方法相同的工具遮挡蒙版。

```bash
# 配置环境
git clone https://github.com/HKU-MedAI/EndoGS.git --recursive
conda create -n endogs python=3.9  
conda env create --file environment.yml
# 单独用pip安装 imageio=2.31.2  lpips=0.1.4
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
git clone --branch depth https://github.com/ingra14m/depth-diff-gaussian-rasterization.git --recursive
git clone https://github.com/facebookresearch/pytorch3d.git

python -c "import torch; print("torch.cuda.is_avaliable()")"
pip install submodules/depth-diff-gaussian-rasterization
pip install submodules/pytorch3d
pip install submodules/simple-knn

# train
python train.py data/endonerf/cutting_tissues_twice/ --workspace output/cutting/
python train.py data/endonerf/pulling_soft_tissues/ --workspace output/pulling/
# inference
python inference.py data/endonerf/cutting_tissues_twice/ --model_path output/cutting/point_cloud/iteration_60000

python inference.py data/endonerf/pulling_soft_tissues/ --model_path output/pulling/point_cloud/iteration_60000
# evaluation
python eval_rgb.py --gt_dir data/endonerf/cutting_tissues_twice/images --mask_dir data/endonerf/cutting_tissues_twice/gt_masks --img_dir output/cutting/point_cloud/iteration_60000/render

python eval_rgb.py --gt_dir .\output\pulling\point_cloud\iteration_60000\gt_choose --mask_dir .\output\pulling\point_cloud\iteration_60000\masks_choose --img_dir .\output\pulling\point_cloud\iteration_60000\render_choose

python eval_rgb.py --gt_dir .\output\cutting\point_cloud\iteration_60000\gt_choose --mask_dir .\output\cutting\point_cloud\iteration_60000\masks_choose --img_dir .\output\cutting\point_cloud\iteration_60000\render_choose
```

