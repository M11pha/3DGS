# 

```bash
bash setup.sh /home/ekko/anaconda3 dgmarbles

bash preprocess_video.sh /home/ekko/github/deformation/dynamic-gaussian-marbles/data/real-world/pulling ~/anaconda3

python train.py --data_dir ./data/real-world/pulling --config configs.dgmarbles_realworld

python mosca_precompute.py --cfg ./profile/demo/demo_prep.yaml --ws ./demo/duck --skip_dynamic_resample

```

```bash
conda create -n pytorch3d python=3.10

pip3 install torch==2.3.1 torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

pip install xformers==0.0.27

pip install "git+https://github.com/facebookresearch/pytorch3d.git"

pip install lib_render/simple-knn
pip install lib_render/diff-gaussian-rasterization-alphadep-add3
pip install lib_render/diff-gaussian-rasterization-alphadep
pip install lib_render/gof-diff-gaussian-rasterization

python run_compute_metrics_som.py --result_dir /home/ekko/github/Deform3DGS/output/endonerf_pro/pulling_fdm/test/ours_3000/renders_de --gt_dir /home/ekko/github/Deform3DGS/output/endonerf_pro/pulling_fdm/test/ours_3000/gt --masks_dir /home/ekko/github/Deform3DGS/output/endonerf_pro/pulling_fdm/test/ours_3000/masks

/home/ekko/github/Deform3DGS/output/endonerf_pro/pulling_fdm/test/ours_3000
```

