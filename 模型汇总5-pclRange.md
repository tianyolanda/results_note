|模型名字| pcl范围 |RPN|w/o ME|AP_CYC |AP_PED|fps|训练命令|
|--- |---|----|----|----|----|----|----|
|people/taAug/48m.FHDP| 48m |RPNV2[128]|N|69.51, 48.90, 42.89 |32.04, 26.80, 23.24|fps|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.taAug/people.fhd.48m.FHDP.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/taAug/48m.FHDP --resume True|
|people/taAug/70m.FHD-again| 70m| RPNV2[128]|N|78.40, 64.38, 59.75 |67.10, 59.94, 53.35|29|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.taAug/people.fhd.70m.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/taAug/70m.FHD-again --resume True|
|[comp0 待训 已写在train.sh里]FHD.rpn1b| 52m |RPNV2[128]|w/o ME|AP_CYC |AP_PED|fps|CUDA_VISIBLE_DEVICES=1 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.taAug/people.fhd.taAug.rpn1b.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/taAug/FHD.rpn1b --resume True|



