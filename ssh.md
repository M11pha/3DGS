# ssh

```python
服务器现在内网地址
ssh端口为22：
4090 Internal IP Address: 10.1.115.28
v100 Internal IP Address: 10.249.67.70

内网地址有时候会跳掉 查询内网地址办法:
浏览器访问39.100.92.125:8100查询v100内网地址
浏览器访问39.100.92.125:8090查询4090内网地址

```



```bash
scp -P 22 -r D:\GitHub\gaussian-splatting\data\cutting_tissues_twice\sparse gouhao@10.1.115.28:/home/gouhao/Github/EndoGS/endo_datasets/EndoNeRF_sample_dataset/cutting_tissues_twice # 从本地上传文件夹至服务器
scp -P 220 C:\Users\61674\.ssh\id_windows_gh.pub gouhao@47.98.186.253:.ssh

scp -P 221 -r gouhao@39.100.92.125:/home/gouhao/Github/DNGaussian/output/llff/flower/render/ours_6000 E:\Github # 从服务器下载文件夹至本地 
```

