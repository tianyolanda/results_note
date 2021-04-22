# bs=4

train_config: {
  optimizer: {
    adam_optimizer: {
      learning_rate: {
        exponential_decay: {
          initial_learning_rate: 0.0002
          decay_length: 0.1
          decay_factor: 0.8
          staircase: True
        }
      }
      weight_decay: 0.0001
    }
    fixed_weight_decay: false
    use_moving_average: false
  }
  steps: 148480 # 92800 # 1856 steps per epoch * 160 epochs
  steps_per_eval: 4640 # 9280 # 1856 steps per epoch * 5 epochs
  save_checkpoints_secs : 1800 # half hour
  save_summary_steps : 10
  enable_mixed_precision: false
  loss_scale_factor: -1
  clear_metrics_every_epoch: true
}


# bs=2

train_config: {
  optimizer: {
    adam_optimizer: {
      learning_rate: {
        exponential_decay: {
          initial_learning_rate: 0.0002
          decay_length: 0.1
          decay_factor: 0.8
          staircase: True
        }
      }
      weight_decay: 0.0001
    }
    fixed_weight_decay: false
    use_moving_average: false
  }
  steps: 371200 # 92800 # 1856 steps per epoch * 160 epochs
  steps_per_eval: 9280 # 9280 # 1856 steps per epoch * 5 epochs
  save_checkpoints_secs : 1800 # half hour
  save_summary_steps : 10
  enable_mixed_precision: false
  loss_scale_factor: -1
  clear_metrics_every_epoch: true
}