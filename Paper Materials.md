# Paper Materials

+ Gaussian Grouping: Segment and Edit Anything in 3D Scenes [ECCV 2024]

    + 基于现有数据集进行重整，添加精细掩码

        > To measure segmentation or fine-grained localization accuracy in open-world scene, ==we evolve the existing LERF-Localization [16] evaluation dataset and propose the LERF-Mask dataset==, where we manually annotate three scenes from LERF-Localization with accurate masks instead of using coarse bounding boxes.

    + 数据集非公共访问权问题

        > To evaluate the reconstruction quality, we tested our Gaussian Grouping on 7 of full 9 sets of scenes presented in Mip-NeRF 360 [1], ==where the flowers and treehill are skipped due to the non-public access right==. We also take diverse 3D scene cases from LLFF [32], Tanks & Temples [18] and Instruct-NeRF2NeRF [12] for visual comparison on scene editing.