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

pip install /home/gouhao/Github/ProPainter/download/torchvision-0.16.0+cu118-cp38-cp38-linux_x86_64.whl

pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
pip3 install torch torchvision torchaudio -i https://mirrors.aliyun.com/pytorch-wheels/cu118
wget https://mirrors.aliyun.com/pytorch-wheels/cu118/torch-2.1.0+cu118-cp38-cp38-linux_x86_64.whl
wget https://mirrors.aliyun.com/pytorch-wheels/cu118/torchaudio-2.1.0+cu118-cp38-cp38-linux_x86_64.whl
wget https://mirrors.aliyun.com/pytorch-wheels/cu118/torchvision-0.16.0+cu118-cp38-cp38-linux_x86_64.whl
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple
wget https://github.com/sczhou/ProPainter/releases/download/v0.1.0/cutie-base-mega.pth
https://github.com/sczhou/ProPainter/releases/download/v0.1.0/i3d_rgb_imagenet.pt
https://github.com/sczhou/ProPainter/releases/download/v0.1.0/ProPainter.pth
https://github.com/sczhou/ProPainter/releases/download/v0.1.0/raft-things.pth
https://github.com/sczhou/ProPainter/releases/download/v0.1.0/recurrent_flow_completion.pth

pip install jinja2==3.1.4 -i https://mirrors.aliyun.com/pypi/simple
# 查看显卡实时状态
watch -n 1 -d nvidia-smi
```

