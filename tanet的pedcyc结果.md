from github

1. Car
Car AP@0.70, 0.70, 0.70:
bbox AP:90.81, 89.56, 87.91
bev  AP:89.90, 86.94, 86.44
3d   AP:88.17, 77.75, 75.31
aos  AP:90.75, 89.18, 87.20
Car AP@0.70, 0.50, 0.50:
bbox AP:90.81, 89.56, 87.91
bev  AP:90.86, 90.25, 89.43
3d   AP:90.85, 90.16, 89.19
aos  AP:90.75, 89.18, 87.20


2.Ped&Cyc (Only one model)
Cyclist AP@0.50, 0.50, 0.50:
bbox AP:86.94, 70.20, 66.22
bev  AP:86.20, 67.70, 63.42
3d   AP:85.21, 65.29, 61.57
aos  AP:86.75, 69.88, 65.89
Cyclist AP@0.50, 0.25, 0.25:
bbox AP:86.94, 70.20, 66.22
bev  AP:86.82, 71.54, 66.99
3d   AP:86.72, 70.49, 65.43
aos  AP:86.75, 69.88, 65.89
Pedestrian AP@0.50, 0.50, 0.50:
bbox AP:70.74, 67.94, 63.76
bev  AP:78.55, 71.41, 66.03
3d   AP:71.04, 64.20, 59.11
aos  AP:52.15, 50.10, 47.10
Pedestrian AP@0.50, 0.25, 0.25:
bbox AP:70.74, 67.94, 63.76
bev  AP:86.90, 82.47, 78.98
3d   AP:86.89, 82.47, 78.96
aos  AP:52.15, 50.10, 47.10


---我测的 (论文里用的这个)
TANet.pp
速度 15.91/s
avg forward time per example: 0.009
avg postprocess time per example: 0.014

Evaluation official
Car AP(Average Precision)@0.70, 0.70, 0.70:
bbox AP:90.73, 89.40, 88.18
bev  AP:90.06, 87.41, 86.99
3d   AP:86.25, 77.20, 75.40
aos  AP:0.55, 1.27, 1.99
Car AP(Average Precision)@0.70, 0.50, 0.50:
bbox AP:90.73, 89.40, 88.18
bev  AP:90.82, 90.10, 89.47
3d   AP:90.82, 90.01, 89.33
aos  AP:0.55, 1.27, 1.99

Evaluation coco
Car coco AP@0.50:0.05:0.95:
bbox AP:72.53, 69.03, 66.84
bev  AP:70.65, 67.31, 65.45
3d   AP:60.13, 55.82, 53.43
aos  AP:0.39, 0.98, 1.51

Cyclist AP@0.50, 0.50, 0.50:
bbox AP:88.14, 70.70, 67.54
bev  AP:84.99, 66.12, 62.62
3d   AP:84.47, 64.08, 59.69
aos  AP:88.04, 70.18, 66.89
Cyclist AP@0.50, 0.25, 0.25:
bbox AP:88.14, 70.70, 67.54
bev  AP:87.66, 70.21, 66.66
3d   AP:87.66, 69.50, 66.19
aos  AP:88.04, 70.18, 66.89
Pedestrian AP@0.50, 0.50, 0.50:
bbox AP:68.30, 64.40, 61.86
bev  AP:75.18, 68.93, 63.91
3d   AP:68.61, 61.33, 55.98
aos  AP:33.82, 33.54, 33.52
Pedestrian AP@0.50, 0.25, 0.25:
bbox AP:68.30, 64.40, 61.86
bev  AP:83.55, 79.80, 76.42
3d   AP:83.55, 79.80, 76.40
aos  AP:33.82, 33.54, 33.52

Cyclist AP@0.50, 0.50, 0.50:
bbox AP:86.10, 68.33, 64.75
bev  AP:84.62, 64.43, 60.38
3d   AP:81.56, 60.62, 56.28
aos  AP:85.91, 67.73, 64.04
Cyclist AP@0.50, 0.25, 0.25:
bbox AP:86.10, 68.33, 64.75
bev  AP:85.65, 67.41, 63.96
3d   AP:85.65, 67.34, 63.59
aos  AP:85.91, 67.73, 64.04
Pedestrian AP@0.50, 0.50, 0.50:
bbox AP:69.93, 66.77, 63.37
bev  AP:76.08, 70.52, 64.93
3d   AP:68.40, 61.74, 56.25
aos  AP:39.41, 39.97, 38.71
Pedestrian AP@0.50, 0.25, 0.25:
bbox AP:69.93, 66.77, 63.37
bev  AP:86.78, 82.10, 78.83
3d   AP:86.78, 82.10, 78.80
aos  AP:39.41, 39.97, 38.71

# COMP1 训的 second.pytorch_TANET 未修改任何参数。refine_weight=2
rb依然不稳定。

Restoring parameters from /home/ogailab/tiatia/codes/TANet/second.pytorch_with_TANet/models/second.pytorch_with_TANet/open_source_train_ped_cyc_tanet_standard_really_psa_weight_2/voxelnet-296960.tckpt
feature_map_size [1, 248, 296]
remain number of infos: 3769
Generate output labels...
[100.0%][===================>][17.86it/s][03:24>00:00]   
generate label finished(18.36/s). start eval:
avg example to torch time: 2.109 ms
avg prep time: 7.484 ms
avg voxel_feature_extractor time = 14.304 ms
avg middle forward time = 0.467 ms
avg rpn forward time = 23.712 ms
avg predict time = 6.196 ms
overall_time: 54.27118137174401
Frame per second (FPS) = 18 fps


Evaluation official
Cyclist AP(Average Precision)@0.50, 0.50, 0.50:
bbox AP:85.86, 66.84, 63.83
bev  AP:84.85, 63.99, 60.89
3d   AP:83.74, 62.06, 58.06
aos  AP:0.95, 4.29, 4.11
Cyclist AP(Average Precision)@0.50, 0.25, 0.25:
bbox AP:85.86, 66.84, 63.83
bev  AP:84.90, 67.17, 63.12
3d   AP:84.90, 66.73, 62.91
aos  AP:0.95, 4.29, 4.11
Pedestrian AP(Average Precision)@0.50, 0.50, 0.50:
bbox AP:63.97, 60.52, 58.45
bev  AP:73.28, 67.65, 62.19
3d   AP:68.02, 61.78, 56.68
aos  AP:26.39, 25.04, 23.45
Pedestrian AP(Average Precision)@0.50, 0.25, 0.25:
bbox AP:63.97, 60.52, 58.45
bev  AP:81.45, 78.58, 75.40
3d   AP:81.44, 78.52, 75.23
aos  AP:26.39, 25.04, 23.45

Evaluation coco
Cyclist coco AP@0.25:0.05:0.70:
bbox AP:82.68, 64.57, 61.55
bev  AP:75.63, 58.08, 54.82
3d   AP:71.09, 53.79, 50.80
aos  AP:0.94, 4.03, 3.93
Pedestrian coco AP@0.25:0.05:0.70:
bbox AP:56.25, 53.92, 51.96
bev  AP:64.54, 60.33, 56.67
3d   AP:58.23, 54.18, 50.63
aos  AP:23.69, 22.50, 21.38



After Refine:
Evaluation official
Cyclist AP(Average Precision)@0.50, 0.50, 0.50:
bbox AP:84.67, 64.42, 61.63
bev  AP:82.74, 61.83, 58.38
3d   AP:81.88, 60.42, 56.27
aos  AP:0.56, 3.61, 3.59
Cyclist AP(Average Precision)@0.50, 0.25, 0.25:
bbox AP:84.67, 64.42, 61.63
bev  AP:83.70, 63.75, 60.37
3d   AP:83.70, 63.64, 60.32
aos  AP:0.56, 3.61, 3.59
Pedestrian AP(Average Precision)@0.50, 0.50, 0.50:
bbox AP:65.26, 62.17, 59.30
bev  AP:73.64, 67.86, 62.67
3d   AP:67.11, 61.39, 55.80
aos  AP:26.76, 25.25, 23.63
Pedestrian AP(Average Precision)@0.50, 0.25, 0.25:
bbox AP:65.26, 62.17, 59.30
bev  AP:83.74, 79.80, 76.94
3d   AP:83.82, 79.80, 76.92
aos  AP:26.76, 25.25, 23.63

Evaluation coco
Cyclist coco AP@0.25:0.05:0.70:
bbox AP:80.32, 62.12, 59.23
bev  AP:73.25, 55.24, 52.36
3d   AP:69.28, 51.86, 49.00
aos  AP:0.56, 3.52, 3.44
Pedestrian coco AP@0.25:0.05:0.70:
bbox AP:58.04, 55.82, 54.01
bev  AP:64.38, 60.40, 56.89
3d   AP:58.45, 54.37, 51.01
aos  AP:24.09, 22.66, 21.47

# 接下来试试second.pytorch_TANET  refine_weight=5的

# pp.TANET rw=2

# pp.TANET rw=5