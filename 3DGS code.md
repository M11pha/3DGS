# E-D3DGS

## 参数设置

```python
lp = ModelParams(parser)
op = OptimizationParams(parser)
pp = PipelineParams(parser)
hp = ModelHiddenParams(parser)
```

### lp 模型参数

```python
class ModelParams(ParamGroup): 
    def __init__(self, parser, sentinel=False):
        self.sh_degree = 3
        self._source_path = ""
        self._model_path = ""
        self._images = "images"
        self._resolution = -1
        self._white_background = True
        self.data_device = "cuda"
        self.eval = True
        self.render_process=False
        self.loader = "colmap"
        self.shuffle = True
        super().__init__(parser, "Loading Parameters", sentinel)

    def extract(self, args):
        g = super().extract(args)
        g.source_path = os.path.abspath(g.source_path)
        return g
```

### op 优化参数

```python
class OptimizationParams(ParamGroup):
    def __init__(self, parser):
        self.dataloader=False
        self.iterations = 30_000
        self.maxtime = 0
        self.position_lr_init = 0.00016
        self.position_lr_final = 0.0000016
        self.position_lr_delay_mult = 0.01
        self.position_lr_max_steps = 20_000
        self.deformation_lr_init = 0.00016
        self.deformation_lr_final = 0.000016
        self.deformation_lr_delay_mult = 0.01
        self.deformation_lr_max_steps = 60_000
        self.batch_size = 1

        self.feature_lr = 0.0025
        self.feature_lr_div_factor = 20.0
        self.opacity_lr = 0.05
        self.scaling_lr = 0.005
        self.rotation_lr = 0.001
        self.percent_dense = 0.01
        self.lambda_dssim = 0.0
        self.lambda_lpips = 0
        self.weight_constraint_init= 1
        self.weight_constraint_after = 0.2
        self.weight_decay_iteration = 5000
        self.opacity_reset_interval = 6000000
        self.densification_interval = 100
        self.densify_from_iter = 500
        self.densify_until_iter = 15_000
        self.densify_grad_threshold_fine_init = 0.0002
        self.densify_grad_threshold_after = 0.0002
        self.pruning_from_iter = 500
        self.pruning_interval = 100
        self.opacity_threshold_fine_init = 0.005
        self.opacity_threshold_fine_after = 0.005
        self.reset_opacity_ratio = 0.
        self.opacity_l1_coef_fine = 0.0001
        
        self.scene_bbox_min = [-2.5, -2.0, -1.0]
        self.scene_bbox_max = [2.5, 2.0, 1.0]
        self.num_pts = 2000
        self.threshold = 3
        self.downsample = 1.0
        
        self.use_dense_colmap = False
        self.use_colmap = False
        self.coef_tv_temporal_embedding = 0
        self.random_until = 10000
        self.num_multiview_ssim = 0
        self.offsets_lr = 0.00002
        self.reg_coef = 1.0
        
        super().__init__(parser, "Optimization Parameters")
```

### pp 流程参数

```python
class PipelineParams(ParamGroup):
    def __init__(self, parser):
        self.convert_SHs_python = False
        self.compute_cov3D_python = False
        self.debug = False
        super().__init__(parser, "Pipeline Parameters")
```

### hp 模型隐藏参数

```python
class ModelHiddenParams(ParamGroup):
    def __init__(self, parser):
        self.net_width = 64
        self.defor_depth = 1
        self.min_embeddings = 30
        self.max_embeddings = 150
        self.no_ds=False
        self.no_dr=False
        self.no_do=True
        self.no_dc=False
        
        self.temporal_embedding_dim=256
        self.gaussian_embedding_dim=32
        self.use_coarse_temporal_embedding=False
        self.no_c2f_temporal_embedding=False
        self.no_coarse_deform=False
        self.no_fine_deform=False
        
        self.total_num_frames=300
        self.c2f_temporal_iter=20000
        self.deform_from_iter=0
        self.use_anneal=True
        self.zero_temporal=False
        super().__init__(parser, "ModelHiddenParams")
```

