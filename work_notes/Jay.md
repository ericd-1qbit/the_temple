  
python applications/densenet_classifier/evaluate_densenet_classifier.py \
    --config-name=benchmarks/benchmark_densenet_normal_cardiomegaly_soft_tissue_mass.yaml \
    general.experiment_tag=test_real_padchest_normal_cardiomegaly_soft_tissue_230331_1_1k_real \
    dataset.dataset_path=./data/padchest_test_train_validation_split_removed_duplicates/test/ \
    dataset.metadata_file=./data/padchest_test_train_validation_split_removed_duplicates/test/metadata.csv \ 
    evaluator.densenet_classifier.trained_classifier_path=./data/training/train_real_padchest_normal_cardiomegaly_soft_tissue_230331_1_1k_real/checkpoints/model-50.pt \
    experiment_mode=test \
    evaluator.densenet_classifier.dataset_type='real' \