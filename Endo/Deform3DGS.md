# Deform3DGS

## 训练流程

```bash
# 默认直接在output文件夹下，train的--expname不用带output
# EndoNeRF
$ python train.py -s data/endonerf/pulling_soft_tissues --expname endonerf/pulling_fdm --configs arguments/endonerf/default.py
$ python render.py --model_path output/endonerf/pulling_fdm  --skip_train --reconstruct_test --configs arguments/endonerf/default.py

$ python train.py -s data/endonerf/cutting_tissues_twice --expname endonerf/cutting_fdm --configs arguments/endonerf/default.py 
$ python render.py --model_path output/endonerf/cutting_fdm  --skip_train --reconstruct_test --configs arguments/endonerf/default.py
$ python metrics.py --model_path output/endonerf/cutting_fdm -p test

# StereoMIS
$ python train.py -s data/StereoMIS/P3/stereo_P3_9100_9467 --expname StereoMIS/p3 --configs arguments/endonerf/default.py 
$ python render.py --model_path output/StereoMIS/p3 --reconstruct_test --configs arguments/endonerf/default.py
$ python metrics.py --model_path output/StereoMIS/p3 -p test
```

## 实验记录

|        Time/Device         |         数据集         |  PSNR  |  SSIM  | LPIPS |  FPS  | Train Time | GPU Memory | 迭代次数 |
| :------------------------: | :--------------------: | :----: | :----: | :---: | :---: | :--------: | :--------: | :------: |
| Paper/NVIDIA RTX A5000 GPU |      EndoNerf * 6      | 37.90  | 0.958  | 0.06  | 338.8 |    64 s    |            |    3K    |
|    24.11.1/4090 Laptop     |    EndoNerf-Cutting    | 38.792 | 0.967  | 0.04  |  373  |    82 s    |     1G     |    3K    |
|    24.11.1/4090 Laptop     |    EndoNerf-Pulling    | 38.325 | 0.961  | 0.064 |  384  |    75 s    |     1G     |    3K    |
|                            |                        |        |        |       |       |            |            |          |
| Paper/NVIDIA RTX A5000 GPU |       StereoMIS        | 30.48  | 0.8274 | 0.21  |  330  |    66s     |            |    3K    |
|    24.11.8/4090 Laptop     | StereoMIS-P3 9100-9467 | 33.005 | 0.868  | 0.175 |  266  |    94s     |    1.5G    |    3K    |