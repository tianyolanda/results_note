|模型名字| RPN |w/o ME|AP_CYC |AP_PED|AP_CAR |AP_VAN| fps|训练命令|
|----|---|----|----|----|----|----|----|----| 
|people/p.ca.rb| PSA[128, 256] |N|AP_CYC |AP_PED|AP_CAR |AP_VAN| fps|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/dc.second/second.psa5.parallel.carb/second/configs/taAug/people.fhd.taAug.rpn2b.config --model_dir /home/ubuntu/codes/3d/dc.second/second.psa5.parallel.carb/models/people/p.ca.rb --resume=True|


