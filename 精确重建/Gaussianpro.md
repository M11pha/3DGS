# Gaussianpro

## 实验记录

|     Time/Device     |    数据集     |  PSNR  | SSIM  | LPIPS | FPS  | Train Time | GPU Memory | 迭代次数 |
| :-----------------: | :-----------: | :----: | :---: | :---: | :--: | :--------: | :--------: | :------: |
|       Paper/        | Waymo-1002751 | 35.97  | 0.959 | 0.207 |      |            |            |          |
| 24.11.6/4090 Laptop | Waymo-1002751 | 34.885 | 0.950 | 0.234 |      |   35min    |     5G     |   30k    |
|                     |               |        |       |       |      |            |            |          |
|                     |               |        |       |       |      |            |            |          |



```bash
python train.py -s ./data/segment-102751 -m ./output --eval --position_lr_init 0.000016 --scaling_lr 0.001 --percent_dense 0.0005 --port 1021 --dataset waymo 
python render.py -m ./output
python metrics.py -m ./output
```

