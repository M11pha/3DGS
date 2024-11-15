# Video Inpainting

```bash
# The first example (object removal)
python inference_propainter.py --video inputs/object_removal/bmx-trees --mask inputs/object_removal/bmx-trees_mask 

python inference_propainter.py --video inputs/object_removal/EndoNeRF_Pulling --mask inputs/object_removal/EndoNeRF_Pulling_mask --height 512 --width 640 --save_frames

python inference_propainter.py --video inputs/object_removal/EndoNeRF_Cutting --mask inputs/object_removal/EndoNeRF_Cutting_mask --height 512 --width 640 --save_frames

python inference_propainter.py --video inputs/object_removal/9060_9320 --mask inputs/object_removal/9060_9320_mask --height 512 --width 640 --save_frames

# The second example (video completion) 
python inference_propainter.py --video inputs/video_completion/running_car.mp4 --mask inputs/video_completion/mask_square.png --height 240 --width 432
```

