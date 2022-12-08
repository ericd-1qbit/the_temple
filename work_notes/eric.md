
  train:
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
    save_and_sample_every: 1
    milestone_sample_image_num: 12
    synthetic_dataset_saving_path: results/synthetic_dataset
    sampled_dataset_saving_path: results/sampled_dataset
    results_folder: results
    learnable_variance: false
    vlb_loss_weight: 0.001
    PYTEST_FOLDER: tests/test_data/cifar10_images
    log_path: results/logs/train.log
    log_loss_lr_every: 50
  hyperparameters:
    train_lr:
    - 0.001
    - 0.002
  evaluation:
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
general:
  random_seed: 42
  experiment_name: synthetic image generation with padchest
  dataset_name: padchest
  use_mlflow: false
  mlflow_run_name_base: train-Unet-35M
  use_profiler: false
  profiler_output_dir: results/profiling/
  distributed: false
  use_hyperopt: false
  set_deterministic_cudnn_algorithms: true
  log_dir_path: results/logs/
  mlflow_tracking_server_host_ip: 127.0.0.1
  mlflow_tracking_server_port: '5000'
