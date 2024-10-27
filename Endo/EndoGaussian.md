# EndoGaussian


## 实验记录

|     Time/Device      |      数据集      |  PSNR  | SSIM  | LPIPS | Train Time | GPU Memory | 迭代次数 |
| :------------------: | :--------------: | :----: | :---: | :---: | :--------: | :--------: | :------: |
|        Paper         |     EndoNerf     | 37.849 | 0.963 | 0.054 |            |            |          |
| 24.10.26/4090 Laptop | EndoNerf-Cutting | 35.808 | 0.956 | 0.102 |   2 min    |    5 GB    |  1K+3K   |
| 24.10.26/4090 Laptop | EndoNerf-Pulling | 35.235 | 0.958 | 0.104 |   3 min    |    3 GB    |  1K+3K   |
|                      |                  |        |       |       |            |            |          |

```bash
# Train
python train.py -s dataset/endonerf/pulling --port 6017 --expname endonerf/pulling --configs arguments/endonerf/pulling.py 
python train.py -s dataset/endonerf/cutting --port 6017 --expname endonerf/cutting --configs arguments/endonerf/cutting.py
# Render
python render.py --model_path output/endonerf/pulling  --skip_train --skip_video --configs arguments/endonerf/pulling.py
python render.py --model_path output/endonerf/cutting  --skip_train --skip_video --configs arguments/endonerf/cutting.py
python render.py --model_path output/endonerf/cutting --skip_train  --configs arguments/endonerf/cutting.py
python render.py --model_path output/endonerf/pulling --skip_train  --configs arguments/endonerf/pulling.py
# Evaluation
python metrics.py --model_path output/endonerf/pulling
python metrics.py --model_path output/endonerf/cutting
```

