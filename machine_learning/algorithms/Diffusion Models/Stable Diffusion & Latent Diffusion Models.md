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



## Blog Notes
- open-source tool
- reverse diffusion: done through a denoising Unet


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

To increase the accessibility of this powerful model class and at the same time reduce its significant resource con- sumption, a method is needed that reduces the computa- tional complexity for both training and sampling. Reducing the computational demands of DMs without impairing their performance is, therefore, key to enhance their accessibility.

we sep- arate training into two distinct phases: First, we train an autoencoder which provides a lower-dimensional (and thereby efficient) representational space which is perceptu- ally equivalent to the data spac

The reduced complex- ity also provides efficient image generation from the latent space with a single network pass. We dub the resulting model class Latent Diffusion Models (LDMs

A notable advantage of this approach is that we need to train the universal autoencoding stage only once and can therefore reuse it for multiple DM trainings or to explore possibly completely different tasks

n sum, our work makes the following contributions:

(i) In contrast to purely transformer-based approaches [23, 66], our method scales more graceful to higher dimen- sional data and can thus (a) work on a compression level which provides more faithful and detailed reconstructions than previous work (see Fig. 1) and (b) can be efficiently applied to high-resolution synthesis of megapixel images. (ii) We achieve competitive performance on multiple tasks (unconditional image synthesis, inpainting, stochastic super-resolution) and datasets while significantly lowering computational costs. Compared to pixel-based diffusion ap-

proaches, we also significantly decrease inference costs. (iii) We show that, in contrast to previous work [93] which learns both an encoder/decoder architecture and a score-based prior simultaneously, our approach does not re- quire a delicate weighting of reconstruction and generative abilities. This ensures extremely faithful reconstructions

and requires very little regularization of the latent space. (iv) We find that for densely conditioned tasks such as super-resolution, inpainting and semantic synthesis, our model can be applied in a convolutional fashion and render

large, consistent images of ∼ 10242 px.  
(v) Moreover, we design a general-purpose conditioning

mechanism based on cross-attention, enabling multi-modal training. We use it to train class-conditional, text-to-image and layout-to-image models.

(vi) Finally, we release pretrained latent diffusion and autoencoding models at https : / / github . com/CompVis/latent-diffusion which might be reusable for a various tasks besides training of DMs [81].



Glossary to check out:
- autoregressive (AR) transformers
	- high-resolution synthesis of complex, natural scenes is presently dominated by scaling up likelihood-based models, potentially containing billions of parameters in
- GANs
	- successes have been revealed to be mostly confined to data with comparably limited variability as their adversarial learning procedure does not easily scale to modeling complex, multi-modal distributions.

Follow ups:
- DDIM?
- Precision and Recall?



