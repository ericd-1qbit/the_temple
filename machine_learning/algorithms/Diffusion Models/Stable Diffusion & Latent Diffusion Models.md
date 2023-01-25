# Stable Diffusion & Latent Diffusion Models
#stablediffusion
https://arxiv.org/abs/2112.10752

## Summary
- training on latent space, not pixel space
- images are compressed/embedded into latent space using a VAE
- diffusion model learns to generate embedded space samples
- these are decoded using the VAE decoder part
- uses CLIP text encoder (details depending on which version one looks at)

### Motivation:
- most pixels in an image are imperceptible details that are semantically meaningless
- unnecessary computation and thus costly training and inference in pixel space

### Procedure
- encode images to latent space via encoder $\varepsilon$
	- reduction factor 8 
	- 3 x 512 x 512 image transformed to 6 x 64 x 64
	- 1/64 memory requirement
	-
- feed into Unet
- decode via decoder $D$
	- sampling: only use decoder



## Paper Reading
- DM - image formation process can be seen as sequential application of denoising AEs
- guiding mechanisms can be used to control image generation process
- training and inference computationally expensive, as operations are done in input space (eg on pixels)
- main idea:
	- apply DM in latent space of powerful, pre-trained autoencoders
- Results:
	- reaching near-optimal retention of detail while reducing complexity
	- state of the art class conditional image synthesis
- Main method:
	- cross-attention layers
	- enable DM to be powerful & flexible generators conditioned on various inputs such as text
----------


Glossary to check out:
- autoregressive (AR) transformers
	- high-resolution synthesis of complex, natural scenes is presently dominated by scaling up likelihood-based models, potentially containing billions of parameters in
- GANs
	- successes have been revealed to be mostly confined to data with comparably limited variability as their adversarial learning procedure does not easily scale to modeling complex, multi-modal distributions.

Follow ups:
- DDIM?
- Precision and Recall?



