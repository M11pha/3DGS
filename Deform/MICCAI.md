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

  