# Depth

## Depth Anything v2

```bash
# 运行命令
python run.py \
  --encoder "vitl" \
  --img-path ./input --outdir ./output \
  --pred-only
  
  python run.py \
  --encoder <vits | vitb | vitl | vitg> \
  --img-path <path> --outdir <outdir> \
  [--input-size <size>] [--pred-only] [--grayscale]
```

## Depth Pro

```bash
# 运行命令
$ depth-pro-run -i ./data/images -o ./output/cutting --skip-display
```

## Depth Any Video

```bash
ssh -p 44139 root@i-2.gpushare.com
etm3U8zC6hucq3GqbpNZ8wSPDpq2ytQY

scp -P 44139 -r E:\Datasets\To_depth_any_video root@i-2.gpushare.com:/root/github/DepthAnyVideo/demos

# 需要改变huaggingface模型下载网站并额外安装ffmpeg
export HF_ENDPOINT=https://hf-mirror.com
sudo apt install ffmpeg
$ python run_infer.py --data_path ./demos/To_depth_any_video/cutting_inpainting.mp4 --output_dir ./outputs/ 
$ python run_infer.py --data_path ./demos/endonerf_video/cutting.mp4 --output_dir ./outputs/ 
```

