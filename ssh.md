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

ssh -P 16743 root@region-46.seetacloud.com

ssh -P 20725 root@connect.westc.gpuhub.com

scp -P 16743 /home/ekko/datasets/MRI/data/data.zip  root@region-46.seetacloud.com:/root/autodl-tmp/HCP-1200
/home/ekko/datasets/MRI
```

```bash
# 恒源云
ssh -p 25790 root@i-1.gpushare.com
4eUv47eGGyUmhXGQuqep9XCmdcCqUxv7

scp -P 25790 stereo_P2_6_10050_10130.zip  root@i-1.gpushare.com:/hy-tmp

ssh -p 38210 root@i-1.gpushare.com
NbxAeKqCN8df57mNWYpgYPd6Twga3n8B
scp -P 38210 F:\Users\Ekko\Downloads\models.zip root@i-1.gpushare.com:/root/models # 从本地上传文件夹至服务器

python ./scripts/commands/SynthSeg_predict.py --i /root/Our_data --o /root/ours_outputs
```



```bash
scp -P 2211 -r E:\Datasets\Experiments\EndoNeRF\EndoGS\cutting\point_cloud\iteration_60000 gouhao@39.100.92.125:/home/gouhao/Github/EndoGS/output/cutting_250208/point_cloud/iteration_60000 # 从本地上传文件夹至服务器
scp -P 220 C:\Users\61674\.ssh\id_windows_gh.pub gouhao@47.98.186.253:.ssh

scp -P 2211 -r gouhao@39.100.92.125:/home/gouhao/Github/EndoGS/output/pulling/point_cloud/iteration_60000/render E:\Datasets\Shapeofmotion\FInal_results\EndoNeRF\EndoGS\R_fu4 # 从服务器下载文件夹至本地 

ssh -p 25790 root@i-1.gpushare.com

scp -P 25790 root@i-1.gpushare.com:/root/ssh/outputs/stereomis/p2_62/checkpoints/model_5000.ckpt /home/ekko/datasets/Shapeofmotion/Ordinal_depth_loss/shape-of-motion/outputs/stereomis/p2_62 # 从服务器下载文件夹至本地 

/home/gouhao/Github/EndoGS/output/cutting_250208/point_cloud/iteration_60000
```

