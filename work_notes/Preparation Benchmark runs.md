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

Our 32 × 32 models use four feature map resolutions (32 × 32 to 4 × 4), and our 256 × 256 models use six.
All models have two convolutional residual blocks per resolution level and self-attention blocks at the 16 × 16 resolution between the convolutional blocks [6]

Our CelebA-HQ/LSUN (2562) models train at 2.2 steps per second at batch size 64, and sampling a batch of 128 images takes 300 seconds.

CelebA-HQ for 0.5M steps

We set T = 1000 without a sweep, and we chose a linear schedule from β1 = 10−4 to βT = 0.02.

We set dropout rate on the other datasets to zero without sweeping.

We also used random horizontal flips for all other datasets except LSUN Bedroom.

-   We set the learning rate to 2 × 10−4 without any sweeping, and we lowered it to 2 × 10−5 for the 256 × 256 images,
-   We set the batch size to 128 for CIFAR10 and 64 for larger images
- -   EMA on model parameters with a decay factor of 0.9999