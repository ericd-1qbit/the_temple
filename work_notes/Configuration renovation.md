
 general:
  experiment_tag: evaluation_tests
  output_directory: results/
  profiler_output_directory: ${output_directory}/profiling/
  logging_output_directory: ${output_directory}/logs/
  training_results_directory: ${output_directory}/training/
  evaluation_results_directory: ${output_directory}/evaluation/
  training_log_file: \${logging_output_directory}/training_\${experiment_tag}.log
  evaluation_log_file: \${logging_output_directory}/evaluation_\${experiment_tag}.log

dataset:
  dataset_name: padchest
  dataset_path: data/padchest/padchest_test
  metadata_file: data/padchest/PADCHEST_chest_x_ray_images_labels_160K_01.02.19.csv

synthetic_dataset:
  dataset_name: padchest_synthetic_5120_v02
  dataset_path: results/synthetic_dataset

trained_diffusion_model:
    model_path: results/checkpoints/model-1.pt

densenet_classifier:
      trained_classifier_path: results/checkpoints/model-1.pt
