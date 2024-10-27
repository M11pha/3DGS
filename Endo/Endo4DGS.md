# Endo4DGS

## 论文实验数据

<table>
  <tr>
    <th rowspan="2">Models</th>
    <th colspan="3">EndoNeRF-Cutting</th>
    <th colspan="3">EndoNeRF-Pulling</th>
    <th rowspan="2">Training Time ↓</th>
    <th rowspan="2">FPS ↑</th>
    <th rowspan="2">GPU Usage ↑</th>
  </tr>
  <tr>
    <th>PSNR ↑</th>
    <th>SSIM ↑</th>
    <th>LPIPS ↓</th>
    <th>PSNR ↑</th>
    <th>SSIM ↑</th>
    <th>LPIPS ↓</th>
  </tr>
  <tr>
    <td>EndoNeRF</td>
    <td>35.84</td>
    <td>0.942</td>
    <td>0.057</td>
    <td>35.43</td>
    <td>0.939</td>
    <td>0.064</td>
    <td>6 hours</td>
    <td>0.2</td>
    <td>4 GB</td>
  </tr>
  <tr>
    <td>EndoSurf</td>
    <td>34.89</td>
    <td>0.952</td>
    <td>0.107</td>
    <td>34.91</td>
    <td>0.955</td>
    <td>0.120</td>
    <td>7 hours</td>
    <td>0.04</td>
    <td>17 GB</td>
  </tr>
  <tr>
    <td>LerPlane-32k</td>
    <td>34.66</td>
    <td>0.923</td>
    <td>0.071</td>
    <td>31.77</td>
    <td>0.910</td>
    <td>0.071</td>
    <td>8 mins</td>
    <td>1.5</td>
    <td>20 GB</td>
  </tr>
  <tr>
    <td><strong>Endo-4DGS</strong></td>
    <td><strong>36.56</strong></td>
    <td><strong>0.955</strong></td>
    <td><strong>0.032</strong></td>
    <td><strong>37.85</strong></td>
    <td><strong>0.959</strong></td>
    <td><strong>0.043</strong></td>
    <td><strong>4 mins</strong></td>
    <td><strong>100</strong></td>
    <td><strong>4 GB</strong></td>
  </tr>
</table>


## 实验记录

|     Time/Device      |      数据集      | PSNR  | SSIM  | LPIPS | 备注 | Train Time | GPU Memory | 迭代次数 |
| :------------------: | :--------------: | :---: | :---: | :---: | ---- | :--------: | :--------: | :------: |
|        Paper         | EndoNerf-Cutting | 36.56 | 0.955 | 0.032 |      |            |            |          |
| 24.10.26/4090 Laptop | EndoNerf-Cutting | 36.41 | 0.954 | 0.034 |      |   5 mins   |    5 GB    |  1K+3K   |
|                      |                  |       |       |       |      |            |            |          |
|        Paper         | EndoNerf-Pulling | 37.85 | 0.959 | 0.043 |      |            |            |          |
| 24.10.26/4090 Laptop | EndoNerf-Pulling | 37.48 | 0.960 | 0.039 |      |   5 mins   |    7 GB    |  1K+3K   |
|                      |                  |       |       |       |      |            |            |          |

```bash
python render.py --model_path output/endonerf/pulling --pc --configs arguments/endonerf.py
python render.py --model_path output/endonerf/cutting --pc --configs arguments/endonerf.py
```

