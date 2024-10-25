# EndoGS

## 实验记录

|      Time/Device       |      数据集      |  PSNR  | SSIM  | LPIPS  |
| :--------------------: | :--------------: | :----: | :---: | :----: |
| 2024.10.25/4090 Laptop | EndoNerf-cutting | 34.623 | 0.947 | 0.0486 |
|                        |                  |        |       |        |
|                        |                  |        |       |        |





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
# inference
python inference.py data/endonerf/cutting_tissues_twice/ --model_path output/cutting/point_cloud/iteration_60000
# evaluation
python eval_rgb.py --gt_dir data/endonerf/cutting_tissues_twice/images --mask_dir data/endonerf/cutting_tissues_twice/gt_masks --img_dir output/cutting/point_cloud/iteration_60000/render

```

