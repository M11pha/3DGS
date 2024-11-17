# Video Inpainting

```bash
# The first example (object removal)
CUDA_VISIBLE_DEVICES=2 python inference_propainter.py --video inputs/object_removal/bmx-trees --mask inputs/object_removal/bmx-trees_mask  --save_frames

CUDA_VISIBLE_DEVICES=2 python inference_propainter.py --video /home/gouhao/dataset/Endo_StereoMIS/Dynamic/stereo_P3_15030_16815/images --mask /home/gouhao/dataset/Endo_StereoMIS/Dynamic/stereo_P3_15030_16815/Inverted_masks --height 512 --width 640 --save_frames --fp16

python inference_propainter.py --video inputs/object_removal/EndoNeRF_Cutting --mask inputs/object_removal/EndoNeRF_Cutting_mask --height 512 --width 640 --save_frames --fp16

python inference_propainter.py --video inputs/object_removal/9060_9320 --mask inputs/object_removal/9060_9320_mask --height 512 --width 640 --save_frames

# The second example (video completion) 
python inference_propainter.py --video inputs/video_completion/running_car.mp4 --mask inputs/video_completion/mask_square.png --height 240 --width 432
```

```

```

