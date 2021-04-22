# 由于exple训出的rb比较稳定,所以用explr训一波people的对比~

|模型名字|  DAug  |RPN| w/o ME|AP_CYC |AP_PED|fps|训练命令|
|--- |---|----|----|----|----|----|----|
|baseline.rpn1b|  ta  |RPNV2[64,128] |N|AP_CYC |AP_PED|fps|训练命令,已写在second.baseline2的train.sh备里|
|baseline.rpn2b|  ta  |RPNV2[128] |N|AP_CYC |AP_PED|fps|训练命令,已写在second.baseline2的train.sh备里|
|tanet.ca      |  ta  |[64,128,256] | N|AP_CYC |AP_PED|fps|训练命令,已写在second.tarpn.norb的train.sh备选里|
|tanet.ca.rb |  ta  |[64,128,256]+ta.rb |N|AP_CYC |AP_PED|fps|训练命令,已写在second.tanet.psa的train.sh里|
|me.rb         |  ta  |PSA[128]  |rb|AP_CYC |AP_PED|fps|训练命令|
|me.ca.dc      |  ta  |PSA[128]  |ca,dc|AP_CYC |AP_PED|fps|训练命令|
|me.ca.dc.rb   |  ta  |PSA[128]  |ca,dc,rb|AP_CYC |AP_PED|fps|训练命令|









- 　感觉作为参数修改的:matchT.nms


# 参考: explr稳定的all


|模型名字|  DAug  |pclR|p/V|max voxel |VFE | MFE | RPN  |w/o ME| AP_CYC| AP_PED|  AP_CAR|AP_VAN |fps|训练命令|
|---|  ----  | ----  |----  |----|----|---- |---- |---- |---- |---- |---- |---- |---- |---- |
|dc2/all/taAug/ca.rb.dc.explr|  ta  |52.8|5| 3w,6w |SVR | FHD | PSA[128]  |ca.rb.dc| 84.83, 63.82, 62.09(rb很稳)| 65.64, 58.53, 52.27(rb很稳)|  88.62, 78.25, 76.83|49.74, 37.29, 31.45 |fps|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/code/tiatia/dc2.second.psa/second/configs/me.all/all.fhd.taAug.me.explr.config --model_dir /home/ogailab/code/tiatia/feifei-models/dc2/all/taAug/ca.rb.dc.explr --resume=True|




