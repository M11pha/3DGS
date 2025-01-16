# ArSSR

```bash
mri_vol2vol  --mov template_brain.nii.gz --o output.mgz --voxsize 1.6


python train.py -encoder_name ResCNN \
                -decoder_depth 8	\
                -decoder_width 256 \
                -feature_dim 256 \
                -hr_data_train /home/ekko/datasets/MRI/data/hr_train \
                -hr_data_val /home/ekko/datasets/MRI/data/hr_val \
                -lr 1e-4 \
                -lr_decay_epoch 200 \
                -epoch 100 \
                -summary_epoch 100 \
                -bs 1 \
                -ss 8000 \
                -gpu 0
                
python train.py -encoder_name ResCNN \
                -decoder_depth 8	\
                -decoder_width 256 \
                -feature_dim 256 \
                -hr_data_train /home/ekko/datasets/MRI/data/fetal_data/train \
                -hr_data_val /home/ekko/datasets/MRI/data/fetal_data/val \
                -lr 1e-4 \
                -lr_decay_epoch 200 \
                -epoch 100 \
                -summary_epoch 100 \
                -bs 1 \
                -ss 8000 \
                -gpu 0
                
encoder_name是编码器网络的类型，包括RDN、ResCNN或SRResNet。
decoder_depth是解码器网络的深度（默认值=8）。
decoder_width是解码器网络的宽度（默认值=256）。
feature_dim是特征向量的维度大小（默认值=128）
hr_data_train是用于训练的 HR 补丁的文件路径（如果使用我们预处理的数据，则可以忽略此项）。
hr_data_val是用于验证的 HR 补丁的文件路径（如果您使用我们的预处理数据，则可以忽略此项）。
lr是初始学习率（默认值=1e-4）。
lr_decay_epoch学习率每隔几个时期乘以 0.5（默认值=200）。
epoch是训练的总次数（默认值 = 2500）。
summary_epoch是每隔几个时期将保存的当前模型（默认值=200）。
bs是 LR-HR 补丁对的数量，即公式 3 中的N （默认值=15）。
ss是采样体素坐标的数量，即公式3中的K （默认值=8000）。
gpu是GPU的数量。

python test.py -input_path /home/ekko/datasets/MRI/data/hr_val \
               -output_path /home/ekko/github/MRI/ArSSR/output \
               -encoder  ResCNN \
               -pre_trained_model ./pre_trained_models/ArSSR_ResCNN.pkl \
               -scale 4 \
               -is_gpu 1 \
               -gpu 0
```

