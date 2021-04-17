
#　dc.psa的各个模型训练及结果记录

##　1. 我整个模型，all类别， config参数没变， 80epoch

CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/all.fhd.me.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all.fhd.mdc.psa --resume=True
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py evaluate --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/all.fhd.me.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all.fhd.mdc.psa --batch_size 1 --measure_time True

速度
generate label finished(27.67/s). start eval:
avg example to torch time: 1.817 ms
avg prep time: 4.287 ms
avg voxel_feature_extractor time = 0.226 ms
avg middle forward time = 16.962 ms
avg rpn forward time = 7.971 ms
avg predict time = 4.625 ms
overall_time: 35.887631094718245
Frame per second (FPS) = 28 fps

结果：people和cyc很不好，car一般。refinement brench（cyc和car）基本都能比原始高，ped一半一半

## (正在训)2.我整个模型，people两个类别， config的优化器+nms参数参照ta的xyres_16改一下， 160epoch，bs4
显存 9511MiB

CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/people.fhd.taparam.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/people.fhd.mdc.psa.taparam --resume=True
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py evaluate --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/people.fhd.taparam.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/people.fhd.mdc.psa.taparam --batch_size 1 --measure_time True


Evaluation official
Cyclist AP(Average Precision)@0.50, 0.50, 0.50:
bbox AP:73.17, 53.18, 51.73
bev  AP:75.73, 52.22, 50.33
3d   AP:74.18, 51.00, 47.92
aos  AP:0.91, 0.78, 0.86
Pedestrian AP(Average Precision)@0.50, 0.50, 0.50:
bbox AP:56.95, 52.81, 48.70
bev  AP:64.98, 56.80, 50.39
3d   AP:59.67, 53.60, 47.79
aos  AP:6.90, 6.56, 6.31

generate label finished(24.47/s). start eval:
avg example to torch time: 1.616 ms
avg prep time: 4.661 ms
avg voxel_feature_extractor time = 0.132 ms
avg middle forward time = 11.803 ms
avg rpn forward time = 17.103 ms
avg predict time = 5.300 ms
overall_time: 40.61513637857496
Frame per second (FPS) = 25 fps


## (待训)3. 我整个模型，all类别， config的优化器+nms参数参照ta的xyres_16改一下， 160epoch
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/all.fhd.tanmsparam.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all.fhd.mdc.psa.taparam --resume=True
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py evaluate --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/all.fhd.tanmsparam.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all.fhd.mdc.psa.taparam --batch_size 1 --measure_time True
