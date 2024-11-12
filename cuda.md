# CUDA

```bash
pip cache purge # 清除pip缓存
# cuDNN
tar -zxvf cudnn-linux-x86_64-8.9.7.29_cuda11-archive.tar.xz

# Linux切换CUDA版本---------------------------------------------------------------------------
stat /usr/local/cuda # 查看当前的软链接
sudo rm -rf /usr/local/cuda
sudo ln -s /usr/local/cuda-11.6 /usr/local/cuda
sudo ln -s /usr/local/cuda-11.8 /usr/local/cuda


pip3 install torch=1.13.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
# 查看显卡实时状态
watch -n 1 -d nvidia-smi
```

