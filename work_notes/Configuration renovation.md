
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





configs.evaluator.densenet_classifier.trained_classifier_path
configs.evaluator.trained_diffusion_model.model_path
config.dataset.dataset_path,