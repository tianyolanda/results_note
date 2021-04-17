# people.fhd.sameAll/noise0.2
16/04/21 comp2

prople sameAll config，只改了noise(0.2,0.2,0.2)

- 命令
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.people/people.fhd.same.asAll.gtnoise0.2.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/people.fhd.sameAll/noise0.2 --resume=True
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py evaluate --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.people/people.fhd.same.asAll.gtnoise0.2.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/people.fhd.sameAll/noise0.2 --batch_size 1 --measure_time True

- 结果 +noise提2个点左右，每个类
Evaluation official
Cyclist AP(Average Precision)@0.50, 0.50, 0.50:
3d   AP:83.18, 64.59, 61.70
还有几个高的
84.05, 63.23, 61.16
84.37, 63.05, 60.92
83.28, 67.18, 61.78

Pedestrian AP(Average Precision)@0.50, 0.50, 0.50:
3d   AP:66.35, 59.77, 53.66

对比了一下，ta的平均和我差不多，ped高2-4个点，cyc高0-2个。而且还需要看到底拿中间的哪个模型。。。

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

# /all.fhd.datap/baseline
事实证明，ta的数据增强几个值的设定，很有效。
以后涉及cyc和ped的训练都用这一套数据增强。起名为datap。
所以我把all.fhd.config的数据增强改成了datap，训练试一下。
但这里次没有放上我自己的改进。且RPNV2是2个block。（）

- 命令
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.all/all.fhd.datap.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all.fhd.datap/baseline --resume=True
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py evaluate --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.all/all.fhd.datap.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all.fhd.datap/baseline --batch_size 1 --measure_time True
