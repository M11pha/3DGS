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
  python run_compute_metrics_som.py --result_dir ./data/cutting/renders --gt_dir ./data/cutting/gt --masks_dir ./data/cutting/masks
  
  
  ```


+ ==重要改动==

  ```bash
  casual_dataset.py Line 507
  F.normalize(original_up.cross(target_up), dim=-1) 
  F.normalize(original_up.cross(target_up, dim=-1), dim=-1) 
  ```

  