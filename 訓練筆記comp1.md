#  me.people/ca.dc.rb.rpn1
16/04/21 comp1
我的全部改進模型（dc用的mmdet的gpu版本），ped和cyc類別.
config用的是目前效果最好的same.asAll
bs=4, 80epo, onecyclelr, 9355MiB 

命令:
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/me.people/me.people.fhd.same.asAll.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.people/ca.dc.rb.rpn1 --resume=True

CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py evaluate --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/me.people/me.people.fhd.same.asAll.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.people/ca.dc.rb.rpn1 --batch_size 1 --measure_time True


- 結果

Cyclist AP(Average Precision)@0.50, 0.50, 0.50:
3d   AP:78.72, 60.48, 57.91

3d   AP:80.43, 59.71, 58.24

Pedestrian AP(Average Precision)@0.50, 0.50, 0.50:
3d   AP:66.58, 60.36, 56.72


[100.0%][===================>][29.38it/s][02:08>00:00]   
generate label finished(29.14/s). start eval:
avg example to torch time: 0.678 ms
avg prep time: 2.011 ms
avg voxel_feature_extractor time = 0.174 ms
avg middle forward time = 20.638 ms
avg rpn forward time = 8.029 ms
avg predict time = 2.595 ms
overall_time: 34.125870372927075
Frame per second (FPS) = 29 fps


# me.people.fhd.same.asAll.rpn2b.config 正在訓練
17/04/21 comp1
和上面的模型比，只是把rpn變成2個block。其他沒變

bs=4, 80epo, onecyclelr,9161MiB

注意，這個channel數要改成256（原來是num_filters[0]，num_filters[0]）
 
        self.concat_conv1 = nn.Conv2d(256, 256, kernel_size=3, padding=1)

命令
CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/me.people/me.people.fhd.same.asAll.rpn2b.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.people/ca.dc.rb.rpn2b --resume=True

CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py evaluate --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/me.people/me.people.fhd.same.asAll.rpn2b.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.people/ca.dc.rb.rpn2b --batch_size 1 --measure_time True
