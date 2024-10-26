# CUDA

```bash
# cuDNN
tar -zxvf cudnn-linux-x86_64-8.9.7.29_cuda11-archive.tar.xz

# Linux切换CUDA版本---------------------------------------------------------------------------
stat /usr/loacl/cuda # 查看当前的软链接
sudo rm -rf /usr/local/cuda
sudo ln -s /usr/local/cuda-10.1 /usr/local/cuda
```

