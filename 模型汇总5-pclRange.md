|模型名字| pcl范围 |w/o ME|AP_CYC |AP_PED|fps|训练命令|
|--- |---|----|----|----|----|----|
|people/taAug/48m.FHDP| 48m |N|69.51, 48.90, 42.89 |32.04, 26.80, 23.24|fps|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.taAug/people.fhd.48m.FHDP.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/taAug/48m.FHDP --resume True|
