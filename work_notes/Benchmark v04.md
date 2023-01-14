python applications/synthetic_image_generation/ddpm_image_generation.py --config-name=realistic_benchmark_padchest_cardiomega
ly_256 experiment_tag=realistic_cardiomegaly_256_v04 trainer.epochs=125

01/14 12:14:02 AM (Elapsed: 00:00:04) Job Configuration:
 general:
  random_seed: 42
  use_profiler: false
  profiler_output_dir: results/profiling/
  distributed: true
  use_hyperopt: false
  set_deterministic_cudnn_algorithms: true
  log_dir_path: results/logs/
  use_mlflow: true
  mlflow_experiment_name: SIG PadChest simplified ${experiment_tag}
  mlflow_run_name_base: train_padchest_unet_114M_${experiment_tag}
  mlflow_tracking_server_host_ip: tracking-server
  mlflow_tracking_server_port: '5000'
architecture:
  first_sample_layer_input_dimension: 256
  input_channels: 1
  inner_layers_dim_mults:
  - 1
  - 1
  - 2
  - 2
  - 4
  - 4
  dropout_rate: 0.0
  use_time_embedding: true
  group_norm_size: 32
  attn_resolutions:
  - 16
  num_res_blocks: 2
  padding: same
  number_classes: 2
  init_conv_kernel_size: 3
  final_conv_kernel_size: 3
  initial_conv_layer_output_channels: 128
  weight_init_method: uniform
  weight_init_gain_factor: 0.02
  learnable_variance: false
dataset:
  differential_diagnoses:
  - pneumonia
  - tuberculosis
  - metastasis
  - lymphangitis
  - lepidic
  - fibrosis
  - post radiotherapy changes
  - asbestosis
  - emphysema
  - COPD
  - heart insufficiency
  - respiratory distress
  - hypertension
  - edema
  artificial_objects: []
  support_devices: []
  pathology_mapping:
    Infiltration:
    - infiltrates
    - interstitial pattern
    - ground glass pattern
    - reticular interstitial pattern
    - reticulonodular interstitial pattern
    - alveolar pattern
    - consolidation
    - air bronchogram
    Pleural_Thickening:
    - pleural thickening
    Consolidation:
    - air bronchogram
    Hilar Enlargement:
    - adenopathy
    - pulmonary artery enlargement
  dataset_name: padchest
  input_image_size: 256
  extensions:
  - jpg
  - jpeg
  - png
  is_class_cond: true
  batch_size: 16
  num_workers: 0
  pin_memory: true
  augment_horizontal_flip: true
  sampler_name: DistributedSampler
  drop_last: true
  dataset_path: data/padchest/padchest_reduced_221208
  metadata_file: data/padchest/PADCHEST_chest_x_ray_images_labels_160K_01.02.19.csv
  pathologies:
  - cardiomegaly
  selected_projections:
  - PA
  - AP
  - AP_horizontal
  age_filter: 10
  unique_patients: false
  shuffle: false
  padchest_path: /home/javad.yaali/padchest_data
  csv_gz_path: /home/javad.yaali/padchest_data/PADCHEST_chest_x_ray_images_labels_160K_01.02.19.csv.gz
  dest_path: data/padchest_xray
  save_reduced_size_images: false
  reduced_size_images_path: data/reduced_size_images
  extract: false
  training_data_path: data/padchest/padchest_reduced_221208
trainer:
  omega: 0.3
  class_cond_drop_out: 0.1
  diffusion_timesteps: 1000
  loss_type: l2
  beta_schedule: linear
  beta_start: 0.0001
  beta_end: 0.02
  ema_decay: 0.9999
  train_lr: 2.0e-05
  epochs: 125
  amp: true
  step_start_ema: 1
  update_ema_every: 1
  save_and_sample_every: 25000
  milestone_sample_image_num: 12
  results_folder: results/${experiment_tag}/
  log_path: results/logs/train_${experiment_tag}.log
  vlb_loss_weight: 0.001
  PYTEST_FOLDER: tests/test_data/cifar10_images
  log_loss_lr_every: 10
evaluator:
  mode: evaluate
  measures:
  - fid_inception
  - fid_densenet121
  run_id: None
  model_path: results/checkpoints/model-1.pt
  distributed: true
  seed: 1
  unnormalize_output: false
  batch_size: 20
  class_label: 0
  log_path: results/evaluation-stats
  sample:
    samples_path: results/sampled_images
    num_samples: 100
  fid_inception:
    type: fid
    num_samples: 6400
    feature_extractor: InceptionV3
    dims: 2048
  fid_densenet121:
    type: fid
    num_samples: 64
    feature_extractor: Densenet121
    weights: densenet121-res224-pc
  ms_ssim:
    type: ms_ssim
    num_samples: 10
hyperparameters:
  train_lr:
  - 0.001
  - 0.002
experiment_tag: realistic_cardiomegaly_256_v04

[W socket.cpp:558] [c10d] The client socket has failed to connect to [localhost]:12355 (errno: 99 - Cannot assign requested address).
[W socket.cpp:558] [c10d] The client socket has failed to connect to [localhost]:12355 (errno: 99 - Cannot assign requested address).
[W socket.cpp:558] [c10d] The client socket has failed to connect to [localhost]:12355 (errno: 99 - Cannot assign requested address).
01/14 12:14:06 AM (Elapsed: 00:00:00) Loaded model and architecture configurations from 'configs/', successfully.
01/14 12:14:10 AM Metadata file has 73509 image entries. Found 73505 in input directory.
01/14 12:14:10 AM (Elapsed: 00:00:04) Created data loader from data/padchest/padchest_reduced_221208 with batch size 16 and image size 256, successfully.
01/14 12:14:12 AM (Elapsed: 00:00:06) Created Unet architecture with input dimension of first downsample layer 256 and depth 6, successfully.
01/14 12:14:16 AM (Elapsed: 00:00:10) Created a U-net with 113670145 number of params
01/14 12:14:23 AM (Elapsed: 00:00:17) Created Synthetic Image Generation model with Unet architecture, successfully.
01/14 12:14:27 AM (Elapsed: 00:00:21) Total number of train_steps 574000 distributed to 4 GPUs.
01/14 12:14:27 AM (Elapsed: 00:00:21) Start training for 143500 number of train_steps on gpu rank cuda:0
01/14 12:14:27 AM (Elapsed: 00:00:21) Epoch: 0 / 125
01/14 12:14:30 AM Reducer buckets have been rebuilt in this iteration.