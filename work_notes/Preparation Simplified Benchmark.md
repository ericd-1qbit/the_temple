
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
  missing_files:
  - 216840111366964012819207061112010307142602253_04-014-084.png
  - 216840111366964012989926673512011074122523403_00-163-058.png
  - 216840111366964012959786098432011033083840143_00-176-115.png
  - 216840111366964012558082906712009327122220177_00-102-064.png
  - 216840111366964012339356563862009072111404053_00-043-192.png
  - 216840111366964013076187734852011291090445391_00-196-188.png
  - 216840111366964012373310883942009117084022290_00-064-025.png
  - 216840111366964012283393834152009033102258826_00-059-087.png
  - 216840111366964012373310883942009170084120009_00-097-074.png
  - 216840111366964012819207061112010315104455352_04-024-184.png
  - 216840111366964013829543166512013353113303615_02-092-190.png
  - 216840111366964012904401302362010337093236130_03-198-079.png
  - 216840111366964012904401302362010336141343749_03-198-010.png
  - 216840111366964012989926673512011151082430686_00-157-045.png
  - 216840111366964012989926673512011083134050913_00-168-009.png
  - 216840111366964012373310883942009077082646386_00-047-124.png
  - 216840111366964013686042548532013208193054515_02-026-007.png
  - 216840111366964013962490064942014134093945580_01-178-104.png
  - 216840111366964012819207061112010281134410801_00-129-131.png
  - 216840111366964013590140476722013043111952381_02-065-198.png
  - 216840111366964012283393834152009027091819347_00-007-136.png
  - 216840111366964012373310883942009152114636712_00-102-045.png
  - 216840111366964012283393834152009033140208626_00-059-118.png
  - 216840111366964013590140476722013058110301622_02-056-111.png
  - 216840111366964012487858717522009280135853083_00-075-001.png
  - 216840111366964013590140476722013049100117076_02-063-097.png
  - 216840111366964013649110343042013092101343018_02-075-146.png
  - 216840111366964012487858717522009280135853083_00-075-001.png
  - 216840111366964012819207061112010306085429121_04-020-102.png
  - 269300710246070740096540277379121868595_e7zsan.png
  - 216840111366964012373310883942009180082307973_00-097-011.png
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
  artificial_objects:
  - artificial
  - surgery
  - metal
  - material
  - sternotomy
  - bone cement
  - prosthesis
  - endoprosthesis
  - foreign body
  - tube
  - stent
  support_devices:
  - device
  - pacemaker
  dataset_name: padchest
  input_image_size: 64
  extensions:
  - jpg
  - jpeg
  - png
  num_class: 1
  is_class_cond: true
  batch_size: 128
  num_workers: 0
  pin_memory: true
  augment_horizontal_flip: true
  sampler_name: DistributedSampler
  drop_last: true
  training_data_path: data/padchest/padchest_reduced_221208
  metadata_file: data/padchest/PADCHEST_chest_x_ray_images_labels_160K_01.02.19.csv
  pathologies:
  - Soft Tissue Mass
  views:
  - PA
  age_filter: 10
  padchest_path: /home/javad.yaali/padchest_data
  csv_gz_path: /home/javad.yaali/padchest_data/PADCHEST_chest_x_ray_images_labels_160K_01.02.19.csv.gz
  dest_path: data/padchest_xray
  save_reduced_size_images: false
  reduced_size_images_path: data/reduced_size_images
  extract: false
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
  amp: true
  step_start_ema: 1
  update_ema_every: 1
  save_and_sample_every: 1000
  milestone_sample_image_num: 12
  synthetic_dataset_saving_path: results/synthetic_dataset
  sampled_dataset_saving_path: results/sampled_dataset
  results_folder: results
  learnable_variance: false
  vlb_loss_weight: 0.001
  PYTEST_FOLDER: tests/test_data/cifar10_images
  log_path: results/logs/train.log
  log_loss_lr_every: 50
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
hyperparameters:
  train_lr:
  - 0.001
  - 0.002