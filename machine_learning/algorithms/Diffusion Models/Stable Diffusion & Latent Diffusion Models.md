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

- excellent blog post: https://medium.com/@steinsfu/stable-diffusion-clearly-explained-ed008044e07e#3608
- open-source tool
- reverse diffusion: done through a denoising Unet
- ![[Pasted image 20230126141503.png]]
![[Pasted image 20230126141636.png]]


![[Pasted image 20230126141719.png]]


As you can see, the diffusing (sampling) process iteratively feeds a full-sized image to the U-Net to get the final result. This makes the pure Diffusion model extremely slow when the number of total diffusing steps **_T_** and the image size are large.

Latent diffusion Models
use encoder to compress full image to latent space
use decoder to reconstruct full image from compressed latent space data


![[Pasted image 20230126141936.png]]
![[Pasted image 20230126142252.png]]

![[Pasted image 20230126142213.png]]

![[Pasted image 20230126142245.png]]
The inner diffusion model is turned into a conditional image generator by augmenting its denoising U-Net with the cross-attention mechanism.

𝜏θ  - language model (BERT, CLIP)
For other spatially aligned inputs (e.g. semantic maps, images, inpainting), the conditioning can be done using concatenation.

![[Pasted image 20230126142850.png]]



![[Pasted image 20230126142928.png]]
![[Pasted image 20230126143203.png]]


![[Pasted image 20230126143212.png]]


### This other blog here
https://towardsdatascience.com/what-are-stable-diffusion-models-and-why-are-they-a-step-forward-for-image-generation-aa1182801d46

Some of the major bottlenecks of the GANs are:

-   Lack of diversity in Image Generation
-   Mode Collapse
-   Problem learning Multimodal distribution
-   High Training Time
-   Not Easy to Train due to the Adversarial Nature of the problem formulation


DM:These models have also been able to produce more diverse images and proved to not suffer from Mode Collapse. This is due to the ability of the _Diffusion Models_ to preserve the semantic structure of the data
Computationally expensiveness:  This is due the fact that all Markovian states need to be in memory for prediction all the time which means multiple instances of large Deep-Nets being present in memory all the time.

 training time for such methods also becomes too high (e.g., days to months) because these models tend to get stuck in the fine-grained _imperceptible_ intricacies in the image data - however, this is also one of their strengths!
 

_Transformers_. They have been highly successful in the language modelling and building conversational AI tools. In vision applications, _Transformers_ have showed advantage of generalization and adaptivity which makes them suitable for general purpose learning. They capture the semantic structure in text and even in images better than other techniques. However, _Transformers_ require huge amount of data and are also facing a plateau in terms of performance in many vision domains compared to other methods.



![[Pasted image 20230126143724.png]]
Stable DM:
 leverages upon the perceptual power of GANs, the detail preservation ability of the _Diffusion Models_, and the Semantic ability of Transformers by merging all three together

They are not only memory efficient compared to the other methods but also produce diverse, highly detailed images which preserve the semantic structure of the data. In short, an _LDM_ is an application of diffusion processes in the latent space instead of pixel space while incorporating the semantic feedback from the _Transformers_.


Any generative learning method has two main stages: Perceptual Compression and Semantic Compression.
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
- check transformer
- 

