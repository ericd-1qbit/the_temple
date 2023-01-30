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


Any generative learning method has two main stages: 

Perceptual Compression - remove high-frequency features and embedd data into absract representation - AE/GANs are good at that

Semantic Compression: - learn conceptual relationships between objects in an image and the semantic context, eg. logical/language meaning
_Transformers_ are good at capturing the semantic structure in text and images. A combination of _Transformers’_ Generalizability and detail preservation ability of the _Diffusion Models_ provides best of both worlds and gives a method ability to generate a fine-grained highly detailed images while preserving the semantic structure in the image.

**Perceptual Loss**

The autoencoder within the LDM is what captures the perceptual structure of the data by projecting the data into latent space. A special loss function is used by authors for training such autoencoder termed, ‘_perceptual loss_’ [4–5]. This loss function ensures that the reconstructions are confined within the image manifold and reduces the blurriness which would otherwise be present when a pixel-space losses are used (e.g., L1/L2 losses).

**Diffusion Loss**

Diffusion models learn a data distribution by gradually removing noise from a normally distributed variable. In other words, DMs employ a reverse _Markov Chain_ of length _T_. This also means that DMs can be modelled as a series of ‘_T’_ denoising autoencoders for time steps _t_ _=1, …,T._ This is represented by the εθ in the following equation. Note that the loss function depends on the latent vector instead the pixel space.
![[Pasted image 20230126145608.png]]


Conditioning:
n order to get the latent representation of this condition as well, a transformer (e.g. CLIP) is used which embeds the text/image into a latent vector ‘τ’.

**Attention Mechanism**

The backbone of an LDM is a U-Net autoencoder with sparse connections providing a cross-attention mechanism [6]. A _Transformer_ network encodes the condition text/image into a latent embedding which is in turn mapped to the intermediate layers of the U-Net via a cross-attention layer. This cross-attention layer implements the attention (**Q,K,V**) = softmax(**QK**T/✔**d**) **V**. Whereas **Q, K** and **V** are learnable projection matrices [6].

Text to image and image to image conditioning.


Wiki-article
Stable Diffusion consists of 3 parts: the [variational autoencoder](https://en.wikipedia.org/wiki/Variational_autoencoder "Variational autoencoder") (VAE), [U-Net](https://en.wikipedia.org/wiki/U-Net "U-Net"), and an optional text encoder
The VAE encoder compresses the image from pixel space to a smaller dimensional [latent space](https://en.wikipedia.org/wiki/Latent_space "Latent space"), capturing a more fundamental semantic meaning of the image.
he U-Net block, composed of a [ResNet](https://en.wikipedia.org/wiki/Residual_neural_network "Residual neural network") backbone, [denoises](https://en.wikipedia.org/wiki/Noise_reduction "Noise reduction") the output from forward diffusion backwards to obtain latent representation
 Finally, the VAE decoder generates the final image by converting the representation back into pixel space
The encoded conditioning data is exposed to denoising U-Nets via a [cross-attention mechanism](https://en.wikipedia.org/wiki/Attention_(machine_learning) "Attention (machine learning)").


The model was trained using 256 [Nvidia A100](https://en.wikipedia.org/wiki/Ampere_(microarchitecture) "Ampere (microarchitecture)") GPUs on [Amazon Web Services](https://en.wikipedia.org/wiki/Amazon_Web_Services "Amazon Web Services") for a total of 150,000 GPU-hours, at a cost of $600,000.[[21]](https://en.wikipedia.org/wiki/Stable_Diffusion#cite_note-21)[[22]](https://en.wikipedia.org/wiki/Stable_Diffusion#cite_note-stable-diffusion-model-card-1-4-22)[[23]](https://en.wikipedia.org/wiki/Stable_Diffusion#cite_note-23)


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




Summary from LilianWeng Blog

- runs the diffusion process in the latent space instead of pixel space
	- making training cost lower
	- inference speed faster. 
- motivation:
	- most bits of an image contribute to perceptual details 
	- semantic and conceptual composition still remains after aggressive compression
- LDM splits up perceptual compression and semantic compression 
	- first remove pixel-level redundancy with autoencoder  by compressing into latent space
	- then manipulate/generate semantic concepts with diffusion process on that learned latent

![[Pasted image 20230130102408.png]]
Illustrating perceptual and semantic compression: Most bits of a digital image correspond to imperceptible details. While DMs allow to suppress this semantically meaningless information by minimizing the responsible loss term, gradients (during train- ing) and the neural network backbone (training and inference) still need to be evaluated on all pixels, leading to superfluous compu- tations and unnecessarily expensive optimization and inference. We propose latent diffusion models (LDMs) as an effective gener- ative model and a separate mild compression stage that only elim- inates imperceptible details.


- perceptual compression - autoencoder model. 
	- An encoder � is used to compress the input image �∈��×�×3 to a smaller 2D latent vector �=�(�)∈�ℎ×�×� , where the downsampling rate �=�/ℎ=�/�=2�,�∈�. 
	- Then an decoder � reconstructs the images from the latent vector, �~=�(�). 

- explored two types of regularization in autoencoder:
	- goal of the regularisation - avoid arbitrarily high-variance in the latent spaces during training

	- VAE inspired KL-regularisation: - KL penalty towards a standard normal distribution over the learned latent
	- VectorQuantisation-reg: withing decoder, like [VQVAE](https://lilianweng.github.io/posts/2018-08-12-vae/#vq-vae-and-vq-vae-2) , quantization layer is absorbed by the decoder.

- denoising model is a time-conditioned U-Net
- augmention with the cross-attention mechanism:
	- handle flexible conditioning information for image generation 
		- (e.g. class labels, semantic maps, blurred variants of an image).
	- each conditioning type paired with a domain-specific encoder �� 
	- projecting the conditioning input � to an intermediate representation 
	- mapped into cross-attention component, ��(�)∈��×��:
