
|COMP |电脑 |内容| 测试方案|目标|
|  ---- |  ----  | ----  |----  |----  |
|0 |我2080 |   all和ped的baseline| 根据ta,second中config的设置区别;找到最好的gt阈值选择,nms, 数据增强,|找到最好的baseline|
|1 |puris 2080ti |dc2.second.psa我的三个改进,对于pedcyc类别效果| |训出最好的baseline|
|2 |飞飞 2080ti || ||


|COMP |0 |1| 2|
|  ---- |  ----  | ----  |----  |
|电脑 |我 |puris| 飞飞|
|显卡 | 2080 | 2080ti | 2080ti|
|源码| second.pytorch.baseline2|dc2.second.psa | dc2.second.psa|
|主要内容| ped cyc all的baseline|我的三个改进,对于pedcyc类别效果 |我的三个改进,对于pedcyc类别效果 |
|测试方案| 根据ta,second中config的设置区别;找到最好的gt阈值选择,nms, 数据增强|用左边找到的最好的config,测我对网络结构的三个改进| 同←|
|目标|找到最好的baseline | 找我网络能work的最好的ap |同←|


# 数据增强方式有三种:

|数据增强方式(DAug)| second.people|second.all| ta |
|  ---- |  ----  | ----  |----  |
|简称| sp|sa| ta |
|groundtruth_localization_noise_std| [0.5, 0.5, 0.3]|[1.0, 1.0, 0.5]| [0.25, 0.25, 0.25]  |
|groundtruth_rotation_uniform_noise| [-0.314, 0.314]|[-0.78539816, 0.78539816]| [-0.15707963267, 0.15707963267] |
|global_translate_noise_std| [0, 0, 0]|[0, 0, 0]| [0.2, 0.2, 0.2] |
|anchor_area_threshold| -1|-1| 1 |



# ped cyc 已训模型汇总(这里的AP一律为最后一个epo的输出结果)
|TANET|AP_CYC| AP_PED|  AP_CAR|
|---|  ----  | ----  |----  |
|TANET.pp|83.40, 62.28, 58.26| 67.29, 60.67, 55.18|  AP_CAR|
|TANET.second|78.59, 57.43, 54.17| 61.88, 56.87, 51.74|  AP_CAR|


|模型名字|  DAug  |pclR|p/V|max voxel |VFE | MFE | RPN  |w/o ME| AP_CYC| AP_PED| 训练命令|
|---|  ----  | ----  |----  |----|---- |---- |---- |---- |---- |---- |---- |
|baseline fhd|  sp  | 48 |5|1.7w,4w | SV | FHDP | RPNV2[128] |N|69.85, 50.35, 48.74| 56.97, 49.03, 46.22|  CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd --resume True|
|matchTlow|  sp | 48 |5|1.7w,4w  |  SV | FHDP | RPNV2[128] |N| 69.73, 49.86, 47.57| 55.85, 48.28, 45.05| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.matchTlow.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.matchTlow --resume True|
|maxV3w|  sp | 48 |5|3w,6w  |  SV | FHDP | RPNV2[128] |N| 69.21, 49.71, 48.55| 56.79, 48.89, 45.83| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.maxV3w.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.maxV3w --resume True|
|nmsLow|  sp | 48 |5|1.7w,4w  |  SV | FHDP | RPNV2[128] |N| 74.58, 49.90, 48.77| 55.29, 47.55, 44.22|  CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.nmsLow.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.nmsLow --resume True|
|fhd.SPMH|  sp  |52.8 |5|1.7w,4w |SVR | FHD | RPNV2[64, 128]  |N| 78.57, 60.58, 54.70| 53.91, 48.49, 42.66|  CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.SPMH.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.SPMH --resume True|
|same.asAll|  ta(no gtnoise)  |52.8|5|3w,6w |SVR | FHD | RPNV2[64, 128]  |N| 83.80, 62.66, 60.27| 65.19, 58.75, 53.01| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.same.asAll.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.same.asAll --resume True|
|same.asAll.SPMFHD.rpn1b|  ta(no gtnoise)  |52.8|5|3w,6w |SV | FHD | RPNV2[128]  |N| 81.09, 65.23, 60.00| 62.29, 54.92, 49.79| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.same.asAll.SPMFHD.rpn1b.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.same.asAll.SPMFHD.rpn1b --resume True|
|same.asAll.SPML.rpn1b|  ta(no gtnoise)  |52.8|1|3w,6w |SVR | FHDL | RPNV2[128]  |N| 79.79, 59.84, 57.92| 57.10, 49.92, 46.21| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.same.asAll.SPML.rpn1b.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.same.asAll.SPML.rpn1b --resume True|
|sameAll.noise0.2|  ta  |52.8|5|3w,6w |SVR | FHD | RPNV2[64, 128]  |N| 83.09, 63.78, 61.91| 66.35, 59.77, 53.66| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.people/people.fhd.same.asAll.gtnoise0.2.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/people.fhd.sameAll/noise0.2 --resume=True|
|fhd.gtnoise0.2(同上)|  ta  |52.8|5|3w,6w |SVR | FHD | RPNV2[64, 128]  |N| 86.02, 71.25, 69.17| 66.30, 59.91, 52.95| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.same.asAll.gtnoise0.2.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.gtnoise0.2 --resume True|
|same.asAll.SPMFHD.rpn1b.SVR|  ta  |52.8|5|3w,6w |SVR | FHD | RPNV2[128]  |N| 80.02, 61.57, 59.61| 64.64, 58.02, 52.10| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.same.asAll.SPMFHD.rpn1b.SVR.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.same.asAll.SPMFHD.rpn1b.SVR --resume True|
|me.ca.dc.rb|  ta(no gtnoise)   |52.8|5|3w,6w |SVR | FHD | PSA[128]  |ca,rb,dc| 78.08, 59.28, 53.59| 59.30, 55.51, 50.20| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/me.people/me.people.fhd.same.asAll.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.people/ca.dc.rb.rpn1 --resume=True|
|me.ca.dc.rb.rpn2b(参数不确定)|  ta(no gtnoise)   |52.8|5|3w,6w |SVR | FHD | PSA[64,128]  |ca,rb,dc| AP_CYC在训| AP_PED在训| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/me.people/me.people.fhd.same.asAll.rpn2b.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.people/ca.dc.rb.rpn2b --resume=True
|
|me.dc|  ta  |52.8|5|3w,6w |SVR | FHD | RPNV2[64, 128]  |N| AP_CYC在训| AP_PED在训| 训练命令|
|taAug/matchT.nms.peoplefhd|  ta  |52.8|5|3w,6w |SVR | FHD  | RPNV2[64, 128]  |N|  AP_CYC在训| AP_PED在训| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.taAug/ta.aug.matchT.nms.peoplefhd.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/taAug/matchT.nms.peoplefhd --resume True
|
|taAug/matchT.nms.ta| ta  |52.8|5|3w,6w |SVR | FHD  | RPNV2[64, 128]  |N| AP_CYC在训| AP_PED在训| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.taAug/ta.aug.matchT.nms.ta.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/taAug/matchT.nms.ta --resume True|



# all已训模型汇总

|模型名字|  DAug  |pclR|p/V|max voxel |VFE | MFE | RPN  |w/o ME| AP_CYC| AP_PED|  AP_CAR|AP_VAN |训练命令|
|---|  ----  | ----  |----  |----|---- |---- |---- |---- |---- |---- |---- |---- |---- |
|baseline fhd|  sa  |52.8|5| 3w,6w |SVR | FHD | RPNV2[64, 128]  |N| 77.94, 60.61, 58.53| 59.90, 52.76, 49.93|88.28, 77.87, 76.05 |50.13, 37.80, 32.29| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/all.fhd.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/all/fhd --resume True|
|all.fhd.datap|  ta  |52.8|5| 3w,6w |SVR | FHD | RPNV2[64, 128]  |N| AP_CYC在训| AP_PED在训|  AP_CAR在训|AP_VAN在训|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.all/all.fhd.datap.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all.fhd.datap/baseline --resume=True
|



