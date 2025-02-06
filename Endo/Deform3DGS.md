# Deform3DGS

## 训练流程

```bash
# 默认直接在output文件夹下，train的--expname不用带output
# EndoNeRF
# Cutting Right View----------------------------------------------------------------
$ python train.py -s data/endonerf_sam/cutting --expname endonerf_sam/cutting --configs arguments/endonerf/default.py

$ python render.py --model_path output/endonerf_sam/cutting  --skip_train --skip_test --reconstruct_video --configs arguments/endonerf/default.py
# ----------------------------------------------------------------------------------
# Pulling Right View----------------------------------------------------------------
$ python train.py -s data/endonerf_sam/pulling --expname endonerf_sam/pulling --configs arguments/endonerf/default.py

$ python render.py --model_path output/endonerf_sam/pulling  --skip_train --skip_test --reconstruct_video --configs arguments/endonerf/default.py
# ----------------------------------------------------------------------------------
# StereoMIS_P1_right_view
$ python train.py -s data/stereomis_sam/stereo_P1_14940_15020 --expname stereomis_sam/P1 --configs arguments/endonerf/default.py
$ python render.py --model_path output/stereomis_sam/P1  --skip_train --skip_test --reconstruct_video --configs arguments/endonerf/default.py

$ python train.py -s data/stereomis_sam/stereo_P2_3_7500_7580 --expname stereomis_sam/P2_3 --configs arguments/endonerf/default.py
$ python render.py --model_path output/stereomis_sam/P2_3  --skip_train --skip_test --reconstruct_video --configs arguments/endonerf/default.py

# ----------------------------------------------------------------------------------
$ python train.py -s data/pulling_soft_tissues --expname endonerf/pulling --configs arguments/endonerf/default.py

$ python train.py -s /home/ekko/datasets/EndoNeRF_PRO/pulling_deblur --expname deblur/pulling --configs arguments/endonerf/default.py

$ python render.py --model_path output/deblur/pulling  --skip_train --reconstruct_test --configs arguments/endonerf/default.py

$ python metrics.py --model_path output/deblur/pulling -p test

$ python train.py -s data/cutting_tissues_twice --expname endonerf/cutting_fdm --configs arguments/endonerf/default.py 

$ python render.py --model_path output/endonerf_pro_inpainting/cutting_fdm   --reconstruct_test --configs arguments/endonerf/default.py

$ python metrics.py --model_path output/endonerf_pro/cutting_fdm -p test
python metrics.py --model_path output/endonerf_pro/pulling_fdm -p test

# StereoMIS
$ python train.py -s /home/ekko/datasets/Shapeofmotion/Right_view/Deform3DGS/data/stereomis_sam/stereo_P3_15140_15230 --expname stereomis_sam/P3 --configs arguments/endonerf/default.py 

$ python render.py --model_path output/stereomis_sam/P3 --skip_train --skip_test --reconstruct_video  --configs arguments/endonerf/default.py

$ python run_compute_metrics_som.py --result_dir ./data/stereomis_p3_right_view/renders --gt_dir ./data/stereomis_p3_right_view/gts --masks_dir ./data/stereomis_p3_right_view/masks

$ python metrics.py --model_path output/StereoMIS/stereo_P3_15140_15230 -p test
$ python run_all.py --data_path Dynamic/stereo_P2_6_9060_9320
$ python run_all.py --dataset_path /home/ekko/datasets/Endo_StereoMIS/Dynamic --subdata_path stereo_P3_15030_16815
$ python run_all.py --dataset_path ./data --subdata_path stereo_P1_14760_15420
```

## 实验记录

|        Time/Device         |                数据集                |  PSNR  |  SSIM  | LPIPS |  FPS  | Train Time | GPU Memory | 迭代次数 |
| :------------------------: | :----------------------------------: | :----: | :----: | :---: | :---: | :--------: | :--------: | :------: |
| Paper/NVIDIA RTX A5000 GPU |             EndoNerf * 6             | 37.90  | 0.958  | 0.06  | 338.8 |    64 s    |            |    3K    |
|    24.11.1/4090 Laptop     |           EndoNerf-Cutting           | 38.792 | 0.967  | 0.04  |  373  |    82 s    |     1G     |    3K    |
|    24.11.1/4090 Laptop     |           EndoNerf-Pulling           | 38.325 | 0.961  | 0.064 |  384  |    75 s    |     1G     |    3K    |
|        Time/Device         |                数据集                |  PSNR  |  SSIM  | LPIPS |  FPS  | Train Time | GPU Memory | 迭代次数 |
| Paper/NVIDIA RTX A5000 GPU |              StereoMIS               | 30.48  | 0.8274 | 0.21  |  330  |    66s     |            |    3K    |
|    24.11.7/4090 Laptop     |      stereo_P1_14760_15420 RAFT      | 30.728 | 0.862  | 0.212 |  277  |    105s    |    1.1G    |    3K    |
|    24.11.8/4090 Laptop     | stereo_P1_14760_15420 depth_anything | 30.775 | 0.861  | 0.220 |  145  |    106s    |    1.1G    |    3K    |
|    24.11.7/4090 Laptop     |      stereo_P2_6_9060_9320 RAFT      | 30.413 | 0.854  | 0.196 |  150  |    96s     |    1.2G    |    3K    |
|    24.11.8/4090 Laptop     | stereo_P2_6_9060_9320 depth_anything | 30.619 | 0.855  | 0.208 |  159  |    103s    |    1.2G    |    3K    |
|    24.11.7/4090 Laptop     |      stereo_P2_6_9400_9900 RAFT      | 27.490 | 0.777  | 0.303 |  238  |    117s    |    1.4G    |    3K    |
|    24.11.8/4090 Laptop     | stereo_P2_6_9400_9900 depth_anything | 27.691 | 0.779  | 0.313 |  208  |    123s    |    1.2G    |    3K    |
|                            |        stereo_P2_6_9950_11100        |        |        |       |       |            |            |          |
|                            |       stereo_P2_6_11300_11850        |        |        |       |       |            |            |          |
|                            |         stereo_P2_7_555_1165         |        |        |       |       |            |            |          |
|                            |         stereo_P3_8980_9900          |        |        |       |       |            |            |          |
|                            |        stereo_P3_10500_11700         |        |        |       |       |            |            |          |
|                            |        stereo_P3_12860_13650         |        |        |       |       |            |            |          |
|                            |        stereo_P3_15030_16815         |        |        |       |       |            |            |          |
|                            |                                      |        |        |       |       |            |            |          |
|                            |                                      |        |        |       |       |            |            |          |
|                            |                                      |        |        |       |       |            |            |          |
|                            |                                      |        |        |       |       |            |            |          |
|    24.11.8/4090 Laptop     |        StereoMIS-P3 9100-9467        | 33.005 | 0.868  | 0.175 |  266  |    94s     |    1.5G    |    3K    |