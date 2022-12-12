
# Configs to set

general:
  experiment_name: synthetic image generation with padchest
  mlflow_run_name_base: train-Unet-35M
architecture:
  input_dimension: 32
  input_channels: 1
  dimension_mults:
  - 1
  - 2
  - 2
  - 2
  dropout_rate: 0.1
  group_norm_size: 32
  attn_resolutions:
  - 16
  num_res_blocks: 2
  weight_init_method: uniform
dataset:
  input_image_size: 64
  num_class: 1
  is_class_cond: true
  batch_size: 128
  augment_horizontal_flip: true
  drop_last: true
  training_data_path: data/padchest/padchest_reduced_221208
  metadata_file: data/padchest/PADCHEST_chest_x_ray_images_labels_160K_01.02.19.csv
  pathologies:
  - Soft Tissue Mass
  views:
  - PA
  age_filter: 10
trainer:
  omega: 0.0
  class_cond_drop_out: 0.1
  diffusion_timesteps: 10
  loss_type: l2
  beta_schedule: linear
  beta_start: 0.0001
  beta_end: 0.02
  ema_decay: 0.9999
  train_lr: 0.0002
  epochs: 1
  step_start_ema: 1
  update_ema_every: 1
  save_and_sample_every: 1000
  milestone_sample_image_num: 12
  synthetic_dataset_saving_path: results/synthetic_dataset
  sampled_dataset_saving_path: results/sampled_dataset
  results_folder: results
  learnable_variance: false
  vlb_loss_weight: 0.001
  log_path: results/logs/train.log
  log_loss_lr_every: 50


%later
evaluator:
  dataset: cifar10
  choices:
  - cifar10
  - celeba_64
  - celeba_256
  - omniglot
  - mnist
  - imagenet_32
  - ffhq
  - lsun_bedroom_128
  - lsun_church_256
  data_path: data
  batch_size: 8
  num_fid_samples: 64
  fid_dir: third_party_utils/nvidia/fid/fid-stats
  distributed: true
  dims: 2048
  seed: 1
  class_label: 0
  log_path: results/logs/validation.log
  model_path: results/checkpoints/model-1.pt
  debug_mode: false
  unnormalize_output: true
  mode: eval_with_fid
  samples_path: results/sampled_images
