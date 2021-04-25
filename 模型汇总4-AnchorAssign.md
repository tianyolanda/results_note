#    anchor_area_threshold: 1 影响了nun_anchors 是否是动态
anchor_area_threshold简称AAT

|模型名字| AAT |RPN|w/o ME|AP_CYC |AP_PED|fps|训练命令|
|--- |---|----|----|----|----|----|----|
|[4/25 白天 COMP0.g0在训]people/taAug/aat1| 1 |RPNV2[128]|N|AP_CYC |AP_PED|fps|CUDA_VISIBLE_DEVICES=0 python ./second/pytorch/train.py train --config_path /home/ubuntu/codes/3d/second.baseline2/second/configs/people.fhd.taAug/people.fhd.aat1.config --model_dir /home/ubuntu/codes/3d/second.baseline2/models/people/taAug/aat1 --resume True|


# anchorAssign有两种方式， 以及对应的matched_threshold，nms_pre_max_size，nms_score_threshold都不同
|模型名字| pcl范围 | anchorA方式|mT|nms_size| nms_score |w/o ME|AP_CYC |AP_PED|fps|训练命令|
|--- |---|----|----|----|----|----|----|----|----|----|
|[4/23 晚 COMP1]fhd.48m.anchorAStride| 48| stride  |0.5,0.35|100,300|0.05,0.5| w/o ME|AP_CYC |AP_PED|fps|python ./second/pytorch/train.py train --config_path /home/ogailab/tiatia/codes/dc2.second.psa-master/second/configs/taAug/people.fhd.48m.anchorAStride.config --model_dir /home/ogailab/tiatia/codes/dc2.second.psa-master/models/me.people/fhd.48m.anchorAStride --resume=True|



1. ta,pp
```buildoutcfg
    anchor_generator_stride: {
              sizes: [0.6, 1.76, 1.73] # wlh
              strides: [0.2, 0.2, 0.0] # if generate only 1 z_center, z_stride will be ignored
              offsets: [0.1, -19.9, -1.465] # origin_offset + strides / 2
              rotations: [0, 1.57] # 0, pi/2
            }
            
        matched_threshold : 0.5
        unmatched_threshold : 0.35
        class_name: "Pedestrian"
        use_rotate_nms: true
        use_multi_class_nms: false
        nms_pre_max_size: 1000
        nms_post_max_size: 100
        nms_score_threshold: 0.4
        nms_iou_threshold: 0.2
```

2. second
```buildoutcfg
     anchor_generator_range: {
          sizes: [0.6, 0.8, 1.73] # wlh
          anchor_ranges: [0, -20, -0.6, 48, 20.0, -0.6] # carefully set z center
          rotations: [0, 1.57] # DON'T modify this unless you are very familiar with my code.
        }
        
        matched_threshold : 0.5
        unmatched_threshold : 0.35
        class_name: "Cyclist"
        use_rotate_nms: false
        use_multi_class_nms: false
        nms_pre_max_size: 1000
        nms_post_max_size: 300
        nms_score_threshold: 0.05
        nms_iou_threshold: 0.5
```
    








