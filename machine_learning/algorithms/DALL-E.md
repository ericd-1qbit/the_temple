# DALL-E
Presentation by Ehsan

## Guided Diffusion
- targets reverse process
- classifier guidance
- use a label to improve
- train another classifier on noisy images with label on images
	- take the log of the prob of that classifier, through the log -> update parameters
	- update mu theta
- class conditioned posterior probability
- ![[Pasted image 20220623102818.png]]
- have to train another model on top... not so good

## Classifier-Free Guidance
- no 