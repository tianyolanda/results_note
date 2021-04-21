
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
|(COMP2)sameAll.noise0.2|  ta  |52.8|5|3w,6w |SVR | FHD | RPNV2[64, 128]  |N| 83.28, 67.18, 61.78| 66.35, 59.77, 53.66| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.people/people.fhd.same.asAll.gtnoise0.2.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/people.fhd.sameAll/noise0.2 --resume=True|
|fhd.gtnoise0.2(同上)|  ta  |52.8|5|3w,6w |SVR | FHD | RPNV2[64, 128]  |N| 82.17, 67.12, 62.10| 66.30, 59.91, 52.95| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.same.asAll.gtnoise0.2.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.gtnoise0.2 --resume True|
|same.asAll.SPMFHD.rpn1b.SVR|  ta  |52.8|5|3w,6w |SVR | FHD | RPNV2[128]  |N| 80.02, 61.57, 59.61| 64.64, 58.02, 52.10| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.same.asAll.SPMFHD.rpn1b.SVR.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/fhd.same.asAll.SPMFHD.rpn1b.SVR --resume True|
|(COMP1)me.ca.dc.rb|  ta(no gtnoise)   |52.8|5|3w,6w |SVR | FHD | PSA[128]  |ca,rb,dc| 78.72, 60.48, 57.91(rb前的結果)| 66.58, 60.36, 56.72(rb前的結果)| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/me.people/me.people.fhd.same.asAll.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.people/ca.dc.rb.rpn1 --resume=True|
|(COMP1)me.ca.dc.rb.rpn2b|  ta(no gtnoise)   |52.8|5|3w,6w |SVR | FHD | PSA[64,128]  |ca,rb,dc|77.91, 60.23, 58.38(rb後的結果，rpn前也差不多)| 64.32, 58.21, 51.90(rb後的結果，rpn前也差不多)| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/me.people/me.people.fhd.same.asAll.rpn2b.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.people/ca.dc.rb.rpn2b --resume=True|
|(COMP2)me.dc|  ta  |52.8|5|3w,6w |SVR | FHD | RPNV2[64, 128]  |N| 82.18, 66.39, 61.08| 67.41, 61.14, 54.31| 训练命令|
|taAug/matchT.nms.peoplefhd|  ta  |52.8|5|3w,6w |SVR | FHD  | RPNV2[64, 128] |dc|  80.70, 62.33, 61.12| 55.05, 49.57, 47.59| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.taAug/ta.aug.matchT.nms.peoplefhd.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/taAug/matchT.nms.peoplefhd --resume True|
|taAug/matchT.nms.ta| ta  |52.8|5|3w,6w |SVR | FHD  | RPNV2[64, 128]  |N| 78.84, 61.04, 57.78| 57.77, 53.08, 48.36| CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.taAug/ta.aug.matchT.nms.ta.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/taAug/matchT.nms.ta --resume True|


# all已训模型汇总

|模型名字|  DAug  |pclR|p/V|max voxel |VFE | MFE | RPN  |w/o ME| AP_CYC| AP_PED|  AP_CAR|AP_VAN |fps|训练命令|
|---|  ----  | ----  |----  |----|----|---- |---- |---- |---- |---- |---- |---- |---- |---- |
|baseline fhd|  sa  |52.8|5| 3w,6w |SVR | FHD | RPNV2[64, 128]  |N| 77.94, 60.61, 58.53| 59.90, 52.76, 49.93|88.28, 77.87, 76.05 |50.13, 37.80, 32.29|没测| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/all.fhd.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/all/fhd --resume True|
|(COMP2)all.fhd.datap|  ta  |52.8|5| 3w,6w |SVR | FHD | RPNV2[64, 128]  |N| 82.81, 68.19, 63.15| 65.41, 59.40, 52.77|  88.91, 78.32, 76.43|51.97, 35.43, 32.16|34|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.all/all.fhd.datap.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all.fhd.datap/baseline --resume=True|
|[在训 COMP1]all/taAug/ca.dc.rb.rpn2b|  ta  |52.8|5| 3w,6w |SVR | FHD | PSA[64,128]  |ca,rb,dc|  AP_CYC| AP_PED|  AP_CAR|AP_VAN |fps|python ./second/pytorch/train.py train --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/taAug/all.fhd.ta.me.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/all/taAug/ca.dc.rb.rpn2b --resume=True|
|[4/20/2021在训 COMP0.g0(刚训完)]all.fhd.taAug.ca.rb.dc.rpn1b|  ta  |52.8|5| 3w,6w |SVR | FHD | PSA[128]  |ca.rb.dc|  79.37, 64.96, 60.06| 64.54, 57.77, 52.48|  88.34, 77.93, 76.61|42.07, 32.10, 29.91 |fps|训练命令|
|(COMP2)all/taAug/ca.rb.dc|  ta  |52.8|5| 3w,6w |SVR | FHD | PSA[128]  |ca.rb.dc|  82.17, 62.54, 59.25(挑最高的,refine不稳定)| 65.31, 59.63, 53.17(挑最高的,refine不稳定)|  AP_CAR|AP_VAN |fps | CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.all/all.fhd.taAug.me.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all/taAug/ca.rb.dc --resume=True|
|[4/21/2021在训 COMP2]dc2/all/taAug/ca.rb.dc.explr|  ta  |52.8|5| 3w,6w |SVR | FHD | PSA[128]  |ca.rb.dc| AP_CYC| AP_PED|  AP_CAR|AP_VAN |fps|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.all/all.fhd.taAug.me.explr.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all/taAug/ca.rb.dc.explr --resume=True|


注:[4/20/2021 在训 COMP0.g1 是second.tanet.psa的psa,用taAug,lr=3,再训练一次]

# car(单class)已训模型汇总

|模型名字|  DAug  |w/o ME|AP_CAR |fps|训练命令|
|---|  ----  |----|----|----|----|
|/taAug/lite|  ta  |N(baseline)| 87.15, 77.34, 75.09 |66| CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/car.taAug/car.lite.taAug.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/car/taAug/lite --resume True|
|car.lite.mdc.psa.moms0.85.taAug|  ta   |ca,rb,dc| 88.30, 78.18, 76.77 |42|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/dc.second/dc2.second.psa/second/configs/taAug/psa.car.lite.taAug.config --model_dir /home/ubuntu/codes/3d/dc.second/dc2.second.test2/models/car.lite.mdc.psa.moms0.85.taAug --resume=True|
|car.lite.rb.taAug|  ta  |rb|87.50, 77.80, 76.44 |47|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/dc.second/dc2.second.psa/second/configs/taAug/psa.car.lite.taAug.config --model_dir /home/ubuntu/codes/3d/dc.second/dc2.second.test2/models/car.lite.rb.taAug --resume=True|
|car.lite.dc.taAug|  ta  |dc| 87.35, 77.48, 75.85 |67?|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/dc.second/dc2.second.psa/second/configs/taAug/psa.car.lite.taAug.ca.dc.config --model_dir /home/ubuntu/codes/3d/dc.second/dc2.second.test2/models/car.lite.dc.taAug --resume=True|
|car.lite.ca.taAug|  ta  |ca| 87.58, 77.63, 76.29 |67|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/dc.second/dc2.second.psa/second/configs/taAug/psa.car.lite.taAug.ca.dc.config --model_dir /home/ubuntu/codes/3d/dc.second/dc2.second.psa/models/car/taAug/lite.ca.taAug --resume=True|
|[待训 COMP0]car.lite.ca.dc.taAug|  ta  |ca,dc|AP_CAR |fps|训练命令|
|[*待训 COMP0]car.lite.各种(ca,rb,dc)排列组合.taAug|  ta  |各种(ca,rb,dc)排列组合|AP_CAR |fps|训练命令|
|----验证refinement brench的补充实验----|  --------  |--------|------- |-------|-------|
|模型名字|  DAug  |w/o ME|AP_CAR |fps|训练命令|
|[4/21/2021在训 COMP0.g1]taAug/ta.norb|  ta  |N(有TA的coarse b)|AP_CAR |fps|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/tt.second/second.tarpn.norb/second/configs/taAug/car.lite.tarpn.norb.config --model_dir /home/ubuntu/codes/3d/tt.second/second.tarpn.norb/model/taAug/ta.norb  --resume True|
|ta.psa.again4.taAug|  ta  |N(有TA的PSA+rb)|87.43, 77.93, 76.08 |45|    train(config_path='/home/ubuntu/codes/3d/tt.second/second.tanet.psa/second/configs/taAug/psa.car.lite.config',model_dir='/home/ubuntu/codes/3d/tt.second/second.tanet.psa/newmodels/ta.psa.again4.taAug',resume=True)|
|model_car.lite.voxelRPN.again3.taAug|  ta  |N(有VoxelRPN的rpn)|88.01, 77.79, 76.29 |没测 命令有错|train(config_path='/home/ubuntu/codes/3d/second.pytorch/second/configs/taAug/car.lite.voxelRPN.config',model_dir='/home/ubuntu/codes/3d/second.pytorch/newmodels/new323/model_car.lite.voxelRPN.again3.taAug',resume=True)|
|[ 4/21/2021在训 COMP0.g0]models-taAug/people/fhd.tapsa|  ta  |N(有TA的PSA)|AP_CAR |fps|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/tt.second/second.tanet.psa/second/configs/taAug/people.fhd.config --model_dir /home/ubuntu/codes/3d/tt.second/second.tanet.psa/models-taAug/people/fhd.tapsa --resume True|


# ped(单class)已训模型汇总

|模型名字|  DAug  | MFE |w/o ME|AP_PED |fps|训练命令|
|---|  ----  |----|----|----|----|----|
|single_class_ped/taAug/fhd|  ta  |RPNV2[64, 128] |N(baseline)|60.67, 57.31, 51.42 |fps|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/single_class_ped/ped.taAug.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/single_class_ped/taAug/fhd --resume True|
|single_class_ped/taAug/fhd.rpn1b|  ta  | RPNV2[128] |N|63.49, 57.69, 51.67 |34|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/single_class_ped/ped.taAug.rpn1b.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/single_class_ped/taAug/fhd.rpn1b --resume True |
|single_class_ped/taAug/fhd.rpn1b.rb|  ta  | PSA[128] |rb|63.51, 58.46, 54.63 |28|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/dc.second/dc2.second.psa/second/configs/single_class_ped/ped.taAug.rpn1b.rb.config --model_dir /home/ubuntu/codes/3d/dc.second/dc2.second.psa/models/single_class_ped/taAug/fhd.rpn1b.rb --resume=True|
|(COMP1)me.single_class_ped/taAug/ca.dc.rb.rpn1b|  ta  | PSA[128] |ca,rb,dc|62.61, 56.59, 50.83 |30|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/taAug/me.single_class_ped.fhd.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.single_class_ped/taAug/ca.dc.rb.rpn1b --resume=True|


# cyc(单class)已训模型汇总

|模型名字|  DAug  | MFE |w/o ME|AP_CYC |fps|训练命令|
|---|  ----  |----|----|----|----|----|
|single_class_cyc/taAug/fhd|  ta  |RPNV2[64, 128] |N(baseline)|80.89, 61.53, 58.28(最高的) |fps|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/single_class_cyc/cyc.taAug.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/single_class_cyc/taAug/fhd --resume True|
|[待训 COMP0]single_class_cyc/taAug/fhd.rpn1b|  ta  | RPNV2[128] |N|AP_PED |fps|训练命令 |
|[待训 COMP0]single_class_cyc/taAug/fhd.rpn1b.rb|  ta  | PSA[128] |rb|AP_PED |fps|训练命令 |
 |可以试试 matchT.nms.peoplefhd参数|  DAug  | MFE |w/o ME|AP_CYC |fps|训练命令|

 