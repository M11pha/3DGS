# 

```bash
bash setup.sh /home/ekko/anaconda3 dgmarbles

bash preprocess_video.sh /home/ekko/github/deformation/dynamic-gaussian-marbles/data/real-world/pulling ~/anaconda3

python train.py --data_dir ./data/real-world/pulling --config configs.dgmarbles_realworld
```

