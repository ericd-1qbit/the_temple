Hints for benchmark:
- x-ray output should be as big as possible, try 256x256
- Network size:
	- similar to celebA, judging from complexity
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




