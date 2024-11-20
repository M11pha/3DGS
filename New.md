# Per Gaussian Deform 3DGS

## EndoNeRF PRO数据集结构

+ **depth** 
  + 由[Depth Any Video with Scalable Synthetic Data](https://arxiv.org/abs/2410.10815)生成的具有一致性的深度图
  + shape : (512, 640)
  + 命名规则`frame-000000-depth.png`
+ **gt_masks** 
  + EndoNeRF自带的工具掩码图
  + shape : (512, 640)
  + 命名规则`frame-000000-gtmask.png`
+ **images**
  + 原始RGB图的左镜头视图（主）
  + shape : (512, 640, 3)
  + 命名规则`frame-000000-color.png`
+ **images_right**
  + 原始RGB图的右镜头视图
  + shape : (512, 640, 3)
  + 命名规则`frame-000000-rcolor.png`
+ **inpainting**
  + 由[ProPainter: Improving Propagation and Transformer for Video Inpainting](https://arxiv.org/abs/2309.03897)生成的去工具图
    + 配合gt_mask
  + shape : (512, 640, 3)
  + 命名规则`frame-000000-inpainting.png`
+ **masks**
  + 由[SAM 2: Segment Anything in Images and Videos](https://arxiv.org/abs/2408.00714)生成的工具掩码图
  + shape : (512, 640)
  + 命名规则`frame-000000-mask.png`

