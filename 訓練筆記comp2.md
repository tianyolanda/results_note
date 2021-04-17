# people.fhd.sameAll/noise0.2
16/04/21 comp2

prople sameAll config，只改了noise(0.2,0.2,0.2)

- 命令
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.people/people.fhd.same.asAll.gtnoise0.2.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/people.fhd.sameAll/noise0.2 --resume=True
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py evaluate --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.people/people.fhd.same.asAll.gtnoise0.2.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/people.fhd.sameAll/noise0.2 --batch_size 1 --measure_time True

- 结果 还可以
Evaluation official
Cyclist AP(Average Precision)@0.50, 0.50, 0.50:
bbox AP:87.03, 72.49, 71.14
bev  AP:84.86, 68.91, 63.90
3d   AP:83.09, 63.78, 61.91
aos  AP:1.05, 3.18, 3.20
Cyclist AP(Average Precision)@0.50, 0.25, 0.25:
bbox AP:87.03, 72.49, 71.14
bev  AP:90.08, 70.98, 68.95
3d   AP:90.08, 70.98, 68.95
aos  AP:1.05, 3.18, 3.20
Pedestrian AP(Average Precision)@0.50, 0.50, 0.50:
bbox AP:70.08, 67.67, 61.75
bev  AP:69.54, 62.73, 59.48
3d   AP:66.35, 59.77, 53.66
aos  AP:7.25, 7.10, 6.65
Pedestrian AP(Average Precision)@0.50, 0.25, 0.25:
bbox AP:70.08, 67.67, 61.75
bev  AP:82.56, 80.34, 73.87
3d   AP:82.53, 80.21, 73.64
aos  AP:7.25, 7.10, 6.65

Evaluation coco
Cyclist coco AP@0.25:0.05:0.70:
bbox AP:85.45, 70.00, 68.23
bev  AP:78.45, 61.46, 58.25
3d   AP:74.05, 57.53, 54.66
aos  AP:1.03, 2.97, 2.93
Pedestrian coco AP@0.25:0.05:0.70:
bbox AP:61.03, 59.35, 55.13
bev  AP:64.06, 59.34, 54.68
3d   AP:59.09, 55.10, 50.16
aos  AP:6.04, 6.07, 5.91

generate label finished(38.68/s). start eval:
avg example to torch time: 1.279 ms
avg prep time: 2.632 ms
avg voxel_feature_extractor time = 0.227 ms
avg middle forward time = 17.281 ms
avg rpn forward time = 2.742 ms
avg predict time = 1.418 ms
overall_time: 25.580251903235357
Frame per second (FPS) = 39 fps


# /people.fhd.sameAll.noise0.2/me.dc

在RPNV2（2个block）里+dc 

bs=4, 80epo, onecyclelr, 4419MiB