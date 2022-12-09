Hints for benchmark:
- x-ray output should be as big as possible, try 256x256
- Network size:
	- similar to celebA, judging from complexity
- might need 1.4million training steps
	- 5k - noise
	- 100k - observe if loss/fid score are improving
	- 800k - current reference runs
- use smoothing for mlflow visualisation
- might need 4-500k more 