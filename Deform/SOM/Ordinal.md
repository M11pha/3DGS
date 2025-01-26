# 顺序深度损失

## Pearson correlation loss

$$
\text{Corr}\left(\hat{D}_t, D_t\right) = \frac{\text{Cov}\left(\hat{D}_t, D_t\right)}{\sqrt{\text{Var}\left(\hat{D}_t\right) \text{Var}\left(D_t\right)}}
$$



## MoDGS - Ordinal Depth Loss

$$
\mathcal{R}\big(D_t(u_1), D_t(u_2)\big) =
\begin{cases}
+1, & D_t(u_1) > D_t(u_2) \\
-1, & D_t(u_1) < D_t(u_2)
\end{cases}
$$

$$
\ell_{\text{ordinal}} = \left\lVert \tanh \left( \alpha \big( \hat{D}_t(u_1) - \hat{D}_t(u_2) \big) \right) - \mathcal{R}\big(D_t(u_1), D_t(u_2)\big) \right\rVert
$$



## Ours

在视频的单目深度估计任务中，如果不同帧之间的深度估计缺乏全局一致的尺度（scale inconsistency），但我们仍希望在相邻帧或者某些关键帧之间保持深度的相对顺序一致（ordinal consistency），可以考虑引入“深度顺序损失”（depth order loss / ordinal loss）

### 为什么需要深度顺序损失

#### 1.单目深度估计的尺度不一致

由于单目深度估计往往只是在单帧或局部时域信息上进行推断，不具备可靠的绝对尺度信息，导致每一帧的深度范围（例如最小深度、最大深度）都可能不一样。这样就可能出现两帧之间同一物体的绝对深度值有较大偏移、甚至缩放不同。

#### 2. 深度顺序信息更稳定

虽然绝对深度值不一定一致，但物体之间的相对远近关系（谁更近、谁更远）在相邻帧中往往不会有大幅度变化（除非出现物体突然遮挡、快速运动、场景变化等极端情况）。因此，如果能维护相邻帧中对应像素/对象的深度顺序一致，就能提高视频深度估计的时空一致性。

### 基于深度顺序一致性的损失设计

假设我们有相邻两帧$I_t$和$I_{t+1}$ ，它们分别被单目深度网络估计为深度图$D_t$和$D_{t+1}$ 。这里$D_{t}(x,y)$表示在第$t$帧中像素$(x,y)$的深度估计值，$D_{t+1}(x^{\prime},y^{\prime})$表示在第$t+1$帧中的相应像素位置的深度估计值。

由于可能存在相机运动或物体运动，需要先找到相邻帧中“匹配”或“对应”的像素（或特征），通常可以通过光流（optical flow）或者特征匹配（feature matching）来获取近似对应关系。例如，通过光流$F_t$，可以把帧$t$中的像素$(x,y)$投影/映射到帧$t+1$中的位置$(x^{\prime},y^{\prime})$。这样，就可以得到同一场景点在两帧上的深度估计值分别是$D_{t}(x,y)$和$D_{t+1}(x^{\prime},y^{\prime})$。

通过对于“错误顺序”进行惩罚来构造损失，对所有符合“在帧$t$中顺序已知”的像素对$(p_1,p_2)$,若在帧$t+1$中顺序出现颠倒或破坏，就要施加额外的损失惩罚，对此我们提出排序损失(Hinge Loss)。
$$
L_{\mathrm{order}} = \left\lVert \sum_{(p_{1},p_{2})\in \mathcal{P}}
 \left| \min\Bigl(
  0,\;
  \epsilon + \bigl(D_{t+1}(p_{1}') - D_{t+1}(p_{2}')\bigr)
          \times \mathrm{sign}\bigl(D_{t}(p_{1})-(D_{t}(p_{2})\bigr)
\Bigr)  \right| \right\lVert
$$

$$
L_{\mathrm{order}} = \left\lVert 
 \min\Bigl(
  0,\;
  \epsilon + \bigl(D_{t+1}(p_{1}') - D_{t+1}(p_{2}')\bigr)
          \times \mathrm{sign}\bigl(D_{t}(p_{1})-(D_{t}(p_{2})\bigr)
\Bigr)   \right\lVert
$$

$$
L_{\mathrm{order}} = \left\lVert 
 \min\Bigl(
  0,\;
  \epsilon + \mathrm{sign}\bigl(\hat{D}_{t}(p_{1}) - \hat{D}_{t}(p_{2})\bigr)
          \times \mathrm{sign}\bigl(D_{t}(p_{1})-(D_{t}(p_{2})\bigr)
\Bigr)   \right\lVert
$$



### 实践要点

1.	像素对应关系获取
•	通常需要一个较为准确的光流估计或特征匹配方法，以保证在帧间建立的像素对应关系是对的，否则会把本不应该对应的像素拿来做顺序对比，容易引入噪声。
2.	只在可靠区域施加顺序约束
•	在出现大遮挡、运动模糊等区域，或者非常远的背景/纹理不明显的区域，深度估计本身就不稳定；并且可能无法准确估计光流。这些区域可以过滤掉，不纳入顺序损失的计算范围。
•	可以基于遮挡检测（occlusion detection）或者光流的反向一致性检查来过滤掉无效区域。
3.	平衡系数与多种损失结合
•	最终的训练通常是多损失项同时加权进行，例如：重投影误差（photometric loss）、平滑度约束（smoothness regularization）、表观一致性（mask / segmentation / normal consistency）等。深度顺序损失只是其中一项，需要通过超参数（权重）来平衡。
4.	避免过强约束
•	在某些情况下，帧间某些局部区域的深度顺序确实可能发生变化（例如快速运动或物体被遮挡后又出现），过分强行维护顺序会导致网络难以学习更复杂的场景动态变化。因此对损失也要有一定的设计，比如采用 hinge loss 时设置合适的 margin，或者只对相对静止或运动一致的像素队列应用顺序约束。

```bash
python run_training.py --work-dir ./outputs/pulling_60_ordinal data:custom --data.seq-name pulling --data.root-dir /hy-tmp/pulling --data.is-train True

python run_val.py --work-dir /home/ekko/datasets/Shapeofmotion/Ordinal_depth_loss/shape-of-motion/model/pulling_60 --model 4000 data:custom --data.seq-name pulling --data.root-dir /home/ekko/datasets/Shapeofmotion/Pulling/pulling_dataset --data.is-train False
```

