# ssh

```python
服务器现在内网地址
ssh端口为22：
4090 Internal IP Address: 10.1.115.28
v100 Internal IP Address: 10.249.67.70

内网地址有时候会跳掉 查询内网地址办法:
浏览器访问39.100.92.125:8100查询v100内网地址
浏览器访问39.100.92.125:8090查询4090内网地址

scp -P 2211 ./Deblur4DGS-ssh.zip gouhao@39.100.92.125:/home/gouhao/Github/Downloads


ssh -p 25790 root@i-1.gpushare.com
scp -P 25790  -r /home/ekko/datasets/Github/Deblur4DGS-ssh.zip  root@i-1.gpushare.com:/root

scp -P 54310  /home/ekko/datasets/MRI/torch-2.2.0+cu121-cp312-cp312-linux_x86_64.whl  root@i-2.gpushare.com:/root/Github/datasets
------------------------------------------------------------------------------------
scp -P 10878 -r //home/ekko/datasets/Ekko_2025/Shape_of_Motion/gsplat  root@i-1.gpushare.com:/root/Github/download

scp -P 56752  /home/ekko/datasets/Ekko_2025/Shape_of_Motion/cutting.zip  root@i-2.gpushare.com:/root/Github/datasets

ssh -p 10878 root@i-1.gpushare.com
# 发送文件到服务器
scp -P 10878 -r /home/ekko/github/deformation/ssh  root@i-1.gpushare.com:/root/Github
scp -P 16743 /home/ekko/datasets/MRI/data/data.zip  root@region-46.seetacloud.com:/root/autodl-tmp/HCP-1200
/home/ekko/datasets/MRI
```

```bash
# 恒源云
ssh -p 25790 root@i-1.gpushare.com
4eUv47eGGyUmhXGQuqep9XCmdcCqUxv7

scp -P 25790 stereo_P2_6_10050_10130.zip  root@i-1.gpushare.com:/hy-tmp


```



```bash
scp -P 2211 /home/ekko/datasets/EndoStereoMIS_Choosed/SoM/stereo_P2_6_10050_10130.zip gouhao@39.100.92.125:/home/gouhao/Github/Downloads # 从本地上传文件夹至服务器
scp -P 220 C:\Users\61674\.ssh\id_windows_gh.pub gouhao@47.98.186.253:.ssh

scp -P 2211 gouhao@39.100.92.125:/home/gouhao/Github/shape-of-motion/outputs/stereomis/p3/checkpoints/model_6000.ckpt /home/ekko/datasets/Shapeofmotion/Ordinal_depth_loss/shape-of-motion/outputs/stereomis/p3/checkpoints # 从服务器下载文件夹至本地 

ssh -p 25790 root@i-1.gpushare.com

scp -P 25790 root@i-1.gpushare.com:/hy-tmp/p2_62_full/checkpoints/model_5000.ckpt /home/ekko/datasets/Shapeofmotion/Ordinal_depth_loss/shape-of-motion/outputs/stereomis/p2_62_full # 从服务器下载文件夹至本地 

```

