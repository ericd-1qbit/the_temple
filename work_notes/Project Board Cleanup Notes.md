- CI with GPUs
- revisit tests

Runtime study of pinned_memory setting
Runtime study of num_workers setting
Runtime study of tensor.to(non_blocking=True) setting#251
batch_size dependence on runtime
Investigate memory usage in detail

Do we need to run the sampling step on all GPUs?
https://github.com/1QB-Information-Technologies/Diffusion-models/issues/253
Remove random_seed and set_random_seed
Add mini-tests for data modules (dataset.py)
Add mini-tests for Unet functions
ParisaZ-1qbit opened about 2 months ago
time_mlp,
up_sample_layers,
down_sample_layers,
mid_layers
Add test for discretized_gaussian_log_likelihood function
Send FID score and best trial to MLflow at the end of running Hyperopt
Move all options aside from the the '*_ADDR' to the config files
add tests for cases when learnable variance is true
ema_rate, decay, beta - harmonise name of variable
Get myself familiar with PyTorch Lightning
Does the interpolation algorithm used for image preparation affect the results? `transforms.Resize( self.image_size, interpolation=transforms.InterpolationMode("bilinear"))`
hydrav0.3: remove all these sub-config splits
