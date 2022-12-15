Hints for benchmark:
- x-ray output should be as big as possible, try 256x256
	- 128 for now
- Network size:
	- similar to celebA, judging from complexity (114M)
- might need 1.4million training steps
	- 5k - noise
	- 100k - observe if loss/fid score are improving
	- 800k - current reference runs
- use smoothing for mlflow visualisation
- might need 400k-500k more trainsteps than tensorflow in pytorch
- switch off Unet dropout
- change Omega parameter (used in sampling)
	- determines the diversity of images (0-1)
	- see classifier-free guidance for reference




save_and_sample_every?


- working on codebase:
- check 
	- tests/profiling/padchest_filters_and_analysis.py
	- configs/dataset/padchest.yaml
	- preprocessors/datasets.py
	- preprocessors/padchest_preparation.py (age_filter)
[preprocessors/padchest_preparation.py](https://github.com/1QB-Information-Technologies/Diffusion-models/pull/618/files/f15e39b857459bf0b4a1bdba40f7a96c44b9d945#diff-c5427a6920793ec2a6438735cbac8b19b0ac2d27c4fad0319b29ae7b396b390a "preprocessors/padchest_preparation.py")
We can mention here that reduced size is 256*256.
We can remove line 11.




Jonathan Ho Reading

- 32x32 models: four feature maps
- 256x256 models: six feature maps
- 16x16 resolution attention blocks
- CelebA-HQ trained for 500k steps

- T = 1000, β1 = 10−4 to βT = 0.02.
- dropout rate CELEBA 0
- random horizontal flips for all datasets except LSUN Bedroom.
- learning rate to 2 × 10−4 without any sweeping
	- lowered to 2 × 10−5 for the 256 × 256 images

- batch size 128 (CIFAR10), 64 (rest) 
- EMA on model parameters with a decay factor of 0.9999

Reference:
Our CelebA-HQ/LSUN (2562) models train at 2.2 steps per second at batch size 64, and sampling a batch of 128 images takes 300 seconds.

CLASSIFIER-FREE DIFFUSION GUIDANCE

https://arxiv.org/pdf/2207.12598.pdf
- best FID results with a small amount of guidance 
	- w = 0.1 or w = 0.3, depending on the dataset)
- the best IS result with strong guidance (w ≥ 4). 
- At w = 0.3, our model’s FID score on 128 × 128 ImageNet outperforms the classifier-guided ADM-G, and at w = 4.0, our model outperforms BigGAN-deep at both FID and IS when BigGAN-deep is evaluated its best-IS truncation level.

We find puncond = 0.5 consistently performs worse than puncond ∈ {0.1, 0.2} across the entire IS/FID frontier; puncond ∈ {0.1, 0.2} perform about equally as well as each other.

T = 256 sampling steps


------------------------

input_dimension: 64
initial_conv_layer_output_channels: 128
input_channels: 1
input_image_size: 128

print(self.mid_block_dim)
512
print(self.layers_in_out_dims)
[(128, 128, 64), (128, 256, 32), (256, 256, 16), (256, 512, 8), (512, 512, 4)]


-------------------
- we set the local batch size per GPU to 60.
- the num parameters does depend on the image size
- 


Setting simplified v01

2/15 05:37:42 PM (Elapsed: 00:00:05) Created data loader from data/padchest/padchest_reduced_221208 with batch size 60 and image size 128, successfully.
12/15 05:37:44 PM (Elapsed: 00:00:06) Created Unet architecture with input dimension (image size) 128 and depth 6, successfully.
12/15 05:37:48 PM (Elapsed: 00:00:10) Created a U-net with 109730305 number of params

simplified v01 w 256 image size
12/15 05:40:10 PM (Elapsed: 00:00:05) Created data loader from data/padchest/padchest_reduced_221208 with batch size 60 and image size 256, successfully.
12/15 05:40:11 PM (Elapsed: 00:00:06) Created Unet architecture with input dimension (image size) 256 and depth 6, successfully.
12/15 05:40:16 PM (Elapsed: 00:00:11) Created a U-net with 113670145 number of params


# Summary External Sources

Jonathan Ho:

CelebA 256x256
114M parameters

total batch size: 64 
lr: 0.00002 (2x10^-5)


Yang Song

CelebA 64x64
total batch size: 128
local batch size: 32
num_steps: 1.3M
lr: 0.0002 (2x10^-4)

CelebA 256x256
total batch size: 64
local batch size: 16
num_steps: 2.4M
lr: 0.00002 (2x10^-5)


----
256 benchmark:

batch size 16
data_points_per_batch = 769
world size 4
epochs 37500