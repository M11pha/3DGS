+ ==更改视角== Deform3DGS/scene/endo_loder.py 217行左右

  ```bash
  # poses
  R, T = self.image_poses[idx]
  
  # here -2时位移为4
  # T[0] -= 2
  
  # fov
  FovX = focal2fov(self.focal[0], self.img_wh[0])
  FovY = focal2fov(self.focal[1], self.img_wh[1])
  ```

  

+ ==计算指标==

  ```bash
  python run_val.py --work-dir /home/ekko/datasets/Shapeofmotion/Ordinal_depth_loss/shape-of-motion/outputs/pulling_depth_test --model 4000 data:custom --data.seq-name pulling --data.root-dir /home/ekko/datasets/Shapeofmotion/Pulling/pulling_dataset --data.is-train False
  # StereoMIS--------------------------------------------------------------------------
  python run_compute_metrics_som.py --result_dir ./data/stereomis_p1/renders --gt_dir ./data/stereomis_p1/gts --masks_dir ./data/stereomis_p1/masks
  
  python run_compute_metrics_som.py --result_dir ./data/stereomis_p2_3/renders --gt_dir ./data/stereomis_p2_3/gts --masks_dir ./data/stereomis_p2_3/masks
  
  python run_compute_metrics_som.py --result_dir ./data/stereomis_p2_6_1/renders --gt_dir ./data/stereomis_p2_6_1/gts --masks_dir ./data/stereomis_p2_6_1/masks
  
  python run_compute_metrics_som.py --result_dir ./data/stereomis_p2_6_2/renders --gt_dir ./data/stereomis_p2_6_2/gts --masks_dir ./data/stereomis_p2_6_2/masks
  
  python run_compute_metrics_som.py --result_dir ./data/stereomis_p3/renders --gt_dir ./data/stereomis_p3/gts --masks_dir ./data/stereomis_p3/masks
  # -----------------------------------------------------------------------------------
  python run_compute_metrics_som.py --result_dir ./data/cutting/renders --gt_dir ./data/cutting/gts --masks_dir ./data/cutting/masks
  
  python run_compute_metrics_som.py --result_dir ./data/cutting-20/renders --gt_dir ./data/cutting-20/gts --masks_dir ./data/cutting-20/masks
  
  python run_compute_metrics_som.py --result_dir ./data/pulling/renders --gt_dir ./data/pulling/gts --masks_dir ./data/pulling/masks
  
  python run_compute_metrics_som.py --result_dir ./data/pulling_full/renders --gt_dir ./data/pulling_full/gts --masks_dir ./data/pulling_full/masks
  
  python run_compute_metrics_som.py --result_dir ./data/cutting_full/renders --gt_dir ./data/cutting_full/gts --masks_dir ./data/cutting_full/masks
  
  python run_compute_metrics_som.py --result_dir ./data/pulling_right_view/renders --gt_dir ./data/pulling_right_view/gts --masks_dir ./data/pulling_right_view/masks
  
  python run_compute_metrics_som.py --result_dir ./data/cutting_right_view/renders --gt_dir ./data/cutting_right_view/gts --masks_dir ./data/cutting_right_view/masks
  ```


+ ==重要改动==

  ```bash
  casual_dataset.py Line 507
  F.normalize(original_up.cross(target_up), dim=-1) 
  F.normalize(original_up.cross(target_up, dim=-1), dim=-1) 
  ```

  