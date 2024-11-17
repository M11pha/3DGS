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
export HF_ENDPOINT=https://hf-mirror.com
$ python run_infer.py --data_path ./demos/wooly_mammoth.mp4 --output_dir ./outputs/ --max_resolution 960
```

