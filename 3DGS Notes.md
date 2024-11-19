# 3DGS Notes

+ 每个像素所做的运算相同，才可以用Pytorch并行化，否则得用CUDA
+ CUDA用block+thread的方式并行化，每个block中可设置很多thread
+ 3DGS将tile设计为block，pixel设计为thread
+ forward和backward的总体思路为将图像分为tile，从global memory取出信息到shared memory，然后计算
+ 一次forward产生一整张图片

## 投影过程

1. 计算投影出来的近似圆的半径 `forward.cu preprocessCUDA`
    + 本为椭圆，近似为圆
2. 计算它覆盖了哪些像素 `forward.cu preprocessCUDA`
    + 分割一张图为很多小格子(**Tile**)，每个Tile为16×16像素，不够的边界处补满
    + 计算圆和哪些格子有交汇，有交汇的格子视为被覆盖

    > 只是以近似圆来快速计算所覆盖的tile，渲染时仍然以椭圆进行
3. 计算每个高斯的前后顺序 `rasterizer_impl.cu InclusiveSum(280) -> SortPairs(311)`

    + tile + gaussian
    + 第一顺序 tile， 第二顺序 近似圆 （32+32）
    + [该部分是除了render之外最耗时的部分](https://github.com/aras-p/UnityGaussianSplatting)
4. 计算每个像素的颜色 `forward.cu renderCUDA(293)`

