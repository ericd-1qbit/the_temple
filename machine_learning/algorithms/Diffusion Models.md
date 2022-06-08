# Diffusion Models
Relates to: [Generative Models]()

| Term                             | Name              | Explanation                                            |
| -------------------------------- | ----------------- | ------------------------------------------------------ |
| $x_0~q(x)$                       | Datapoint         | Real sample of dataset                                 |
| $\{\beta_t \in (0, 1)\}_{t=1}^t$ | Variance Schedule | Step sizes defining how much noise is added at steps t |
|                                  |                   |                                                        |

## In short:
- Kind of generative model relying on Markov chains
- 2 steps: 
	- forward diffusion - add random noise to given data
	- reverse diffusion - reconstruct/generate data from noisy sample
![Pasted image 20220601150447.png](app://local/Users/ericdrechsler/codez/the_temple/Pasted%20image%2020220601150447.png?1654121087214)

### Forward Diffusion

1. sample datapoint from data distribution $$x_0\sim q(x)$$
2. Produce successively noisier samples $x_0,x_1,...,x_T$ . 
	1.  The amount of noise added at each step is determined by variance schedule $$\{\beta_t \in (0, 1)\}_{t=1}^T$$
	2.  The distribution for a single sample step is therfore given by $$q(x_t|x_{t-1})=\mathcal{N}(x_t;\sqrt{1-\beta_t}x_{t-1},\beta_t)$$
3. The #reparameterization Trick can be used to do this sampling, thereby enabling to learn the distributions in backpropagation.
	1. Draw random variable $$z_{t-1}\sim\mathcal{N}(0,I)$$from standard normal gaussian.
	2. With $$\alpha_t = 1 - \beta_t; \bar{\alpha}_t = \prod_{i=1}^T \alpha_i$$ we can sample $x_t$ k like so: $$\begin{aligned}
\mathbf{x}_t 
&= \sqrt{\alpha_t}\mathbf{x}_{t-1} + \sqrt{1 - \alpha_t}\mathbf{z}_{t-1} & \text{ ;where } \mathbf{z}_{t-1}, \mathbf{z}_{t-2}, \dots \sim \mathcal{N}(\mathbf{0}, \mathbf{I}) \\
&= \sqrt{\alpha_t \alpha_{t-1}} \mathbf{x}_{t-2} + \sqrt{1 - \alpha_t \alpha_{t-1}} \bar{\mathbf{z}}_{t-2} & \text{ ;where } \bar{\mathbf{z}}_{t-2} \text{ merges two Gaussians (*).} \\
&= \dots \\
&= \sqrt{\bar{\alpha}_t}\mathbf{x}_0 + \sqrt{1 - \bar{\alpha}_t}\mathbf{z} \\
q(\mathbf{x}_t \vert \mathbf{x}_0) &= \mathcal{N}(\mathbf{x}_t; \sqrt{\bar{\alpha}_t} \mathbf{x}_0, (1 - \bar{\alpha}_t)\mathbf{I})
\end{aligned}$$

3. The final noisy sample distribution is thereby given by $$q(x_{1:T}|x_0)=\prod_{t=1}^{T}{q(x_t|x_{t-1})}$$
   The data sample loses it's distinguishable features with progressive t and for $T\rightarrow\inf$ becomes equivalent to an isotropic Gaussian distribution. 
### Reverse Diffusion
1. Reverse the diffusion steps starting from a noisy sample $$x_T\sim\mathcal{N(0,I)}$$
2. It is hard to estimate $q(x_{t-1}|x_{t})$ true conditional distribution. Find an approximate conditional distribution $$p_\theta(x_{0:T})=p(x_T)\prod_{t=1}^{T}{p_\theta(x_{t-1}|x_t)}$$ where $$p_\theta(x_{t-1}|x_t)=\mathcal{N}(x_{t-1};\mu_\theta(x_t,t),\Sigma_\theta(x_t,t))$$
3. Use the Kullback-Leibler Divergence $D_{KL}$ to quantify the distance between the approximate and true conditional distribution $$D_{KL}(q(x_{1:T}|x_0)||p_\theta(x_{1:T}|x_0)))$$
	1. Conditioning the true distr on $x_0$ makes it tractable.
	2. 
4. Calculate Loss function using the same strategy as in a VAE.

### Loss Function
Variational Lower Bound:
$$L_{VLB}=\mathbb{E}_q(x_{0:T})\left[\log{\frac{q(x_{1:T|x_0})}{p_\theta(x_{0:T})}}\right]$$
This can be rewritten as a sum of Kullback-Leibler Divergences of all Markov-Chain terms:

$$\begin{align}
L_{VLB} &= L_0+\sum_{t=1}^{T-1}L_t+L_T\\
(L_0) &= -\log{p_\theta(x_0|x_1)}\\
(L_t) &+ \sum_{t=1}^{T-1} D_{KL}(q(x_t|x_{t+1},x_0)||p_\theta(x_t|x_{t+1}))\\
(L_T) &+ D_{KL}(q(x_T|x_0)||p_\theta(x_T))
\end{align}$$
Simplifications to this loss function are available.


### Algorithm
Denoising Diffusion Probabilistic Models
https://arxiv.org/abs/2006.11239

![[Pasted image 20220601154435.png]]

## Applications
##### Image Generation
- Task:
	- generate synthetic images from specific distributions learned in given dataset 
- Method:
	- Reconstruction Loss like MSE and variational lower bound (VLB) $$L_{MSE}+\lambda L_{VLB}$$
- Datasets: ImageNet, LSUN
- Benchmarks: Google Open Images, CelebA-HQ

##### Image Segmentation
- Task:
	- assign each pixel in image a label to classify if pixel belongs to specific class
	- used for: 
		- object recognition
		- occlusion boundary estimation
		- image compression/editing
- Method:
	- Diffusion method for image segmentation (Tomer et al., 2021)
- Datasets: Cityscape, Vaihingen, MoNuSeg
- Benchmarks: Google open images, SYNTHIA

##### Image-to-Image Translation
- Task: Transforming an image from one domain to another.
- Examples: Style transfer, super-resolution and colourization
- Method: UNpaired Image Translation with Denoising Diffusion Probabilistic Models (UNIT-DDPM) (Sasaki et al., 2021)
-   Datasets: Facades, Photo-Maps, Summer-Winter, RGB-Thermal
-   Potential benchmarks: ImageNet (translation between two similar categories)

##### Medical Anomaly Detection

-   Task: To create an anomaly map from input images based on the image-to-image translation (Wolleb et al. ).
-   Examples: Find anomalies on the medical images.
-   Method: Generating the image without any pathologies using diffusion models and subtract it from input image in order to create anomaly map.
-   Datasets: cheXpert, BraTS
-   Potential benchmarks: OASIS-3, XrAI (Synthesis Health)

##### Audio Generation
-   Task: Generating raw audio such as speech
-   Examples: Text-to-speech, music, speech enhancement, voice conversion, creative sound design for music and film.
-   Method: DiffWave which is a versatile diffusion
    model for audio synthesis (Kong et al., 2021).
-   Datasets: LJ speech, Speech Commands
-   Potential benchmarks: English multi-speaker
    corpus from CSTR voice cloning toolkit (VCTK)
###### Text-to-Speech
• Task: Generating synthesized speech from text.
• Examples: Helping users with disabilities, banking,
media, entertainment, health care, home
automation.
• Method: InferGrad which improves diffusion
models for vocoder (Chen et al., 2022)
• Datasets: LJ Speech dataset
• Potential benchmarks: LibriTTS

##### Time series forecasting

- Task: generating missing values in a time series based on the observed samples.  
- Examples: Find missing values in time series, forecasting time series.  
- Method: Using conditional score based diffusion model.  
- Datasets: PhysioNet, Air quality  
- Potential benchmarks: ETT, whether

##### Attack detection for cyber-physical systems

-   Task: Real-time attack detection based on the historical data.
-   Examples: Find anomalies on the cybersecurity platforms.
-   Method: Predicting the pattern based on the historical data using diffusion models. Then, compare it with the observed value in order to detect anomalies.
-   Datasets: PUMP, SWAT, WADI
-   Potential benchmarks: KDDCUP

##### Video Generation

-   Task: Stochastic video generation.    
-   Examples: Stochastic video generation and
    forecasting is important in various contexts; e.g. model-based reinforcement learning, data-driven weather prediction, and neural video compression.
-   Method: A denoising process generates residuals to refine the output from autoregressive model for error correction and improves sample quality.
-   Dataset: BAIR Robot arm, KTH Actions, City scape,a two-dimensional Simulation dataset for turbulent flow
-   Potential benchmarks: UCF101, Kinetics-600


## Further Reading
##### Changing loss functions
-  DDPMs require a large number of iterations in inference → slow inference speed
-  InferGrad:
    -  Incorporates inference process into training → keep quality with reduced number of iterations
    -  Add another loss term (inference loss) based on the Fourier feature of the input signal 
-  VDM:
    -  Learning noise schedule
    -  Add Fourier feature of the signal into the noise prediction network.

##### Improving Sampling speed
- Drawback of the DDPMs → requiring a huge number of refinement steps  
- Itô-Taylor Sampling Scheme:
	-  The idea for the proposed solution is based on ideal derivative substitution.
	-  Second order sampler for existing DDPM models, which enables faster sampling than existing first order counterparts (Euler-Maruyama schemes).
    Song et al., 2021:  
    -   Leverage an ODE solver to accelerate the sampling procedure.
    -   Combining CSDI with this method would likely improve the sampling efficiency

##### Changing noise distribution
-   A notable property of the diffusion process is a closed-form formulation of the noise
-  Gamma distribution: 
    -  The idea for the proposed solution is sum of two distributions that share the scale parameter is a Gamma distribution of the same scale. 
    - Gamma is better suited to fit the data than a Gaussian distribution.
    - Gamma can help speed up the convergence of the DDPM.
    
##### Diffusion Priors for Variational Autoencoders

-  Variational autoencoders (VAEs) offer scalable amortized posterior inference and fast sampling.
-  In the original formulation of VAEs, the prior and the posterior distributions over the latent variables are assumed to be Gaussian.
-  Whenkel and Louppe (2021) improve VAEs by using DDPMs for modelling the prior distribution of the  latent variables.
    -  Recent advances in DDPM can be incorporated into the prior model.
    -  Image synthesis with hierarchical VAEs could benefit from the diffusion priors.

##### Distributed ML

-  Distributed machine learning is a multi-node ML system that improves performance, increases accuracy, and scales to larger input data sizes. 
-  Accelerate the training of the diffusion models by using multi GPU
-  We implement DDPM with Unet model (here) for noise prediction on CelebA dataset:
 Single Node: 1 x Tesla T4, 100GB SSD storage, 192GB RAM, 48 vCPU
	 Runtime for 5000 training steps: 4h 9 min  
Multi Node: 4 x Tesla T4, 100GB SSD storage, 192GB RAM,
48 vCPU  
	Runtime for 5000 training steps: 1h 34 min

## Sources

### Repositories
- [Examples of Diffusion Model Applications](https://github.com/heejkoo/Awesome-Diffusion-Models)
- [Denoising Diffusion in pytorch](https://github.com/lucidrains/denoising-diffusion-pytorch/)

##### Tensorflow
- [Denoising Diffusion Probabilistic Models (DDPM)](https://github.com/hojonathanho/diffusion)
- [DiffWave: A Versatile Diffusion Model for Audio Synthesis](https://github.com/revsic/tf-diffwave)

##### PyTorch
- [Guided diffusion](https://github.com/openai/guided-diffusion)
- [Text to image & impainting](https://github.com/CompVis/latent-diffusion)
- [Simple DDPM](https://github.com/lucidrains/denoising-diffusion-pytorch)
- [Notebook DDPM](https://github.com/acids-ircam/diffusion_models)
- [Diffusion-CLIP](https://github.com/gwang-kim/DiffusionCLIP)
- [Palette](https://paperswithcode.com/paper/palette-image-to-image-diffusion-models-1)
##### Applications
- [Image-to-Image Translation](https://github.com/weihaox/awesome-image-translation)
- [Contrastive Unpaired Translation](https://github.com/taesungp/contrastive-unpaired-translation)
	- State of the art image-to-image translation
- [UNIT-DDPM: UNpaired Image Translation with Denoising Diffusion Probabilistic Models](https://arxiv.org/abs/2104.05358)

### Papers
#### Diffusion Models
 - [Improved Denoising Diffusion Probabilistic Models](https://arxiv.org/abs/2102.09672)
	 - heavily referenced
 - [Deep Unsupervised Learning using Nonequilibrium Thermodynamics](https://arxiv.org/abs/1503.03585)
	- First paper on the topic

##### Applications
- [Contrastive Unpaired Translation](https://arxiv.org/abs/2007.15651)
	- State of the art image-to-image translation
- [Image-to-Image Translation: Methods and Applications](https://arxiv.org/abs/2101.08629)
- [conditional diffusion models - Palette: Image-to-Image Diffusion Models](https://arxiv.org/abs/2111.05826)
	- https://paperswithcode.com/paper/palette-image-to-image-diffusion-models-1


##### Related
- [Ab-Initio Solution of the Many-Electron Schrodinger Equation with Deep Neural Networks](https://arxiv.org/abs/1909.02487)
	- -   related optimization algorithm:
    

-   [http://proceedings.mlr.press/v37/martens15.html](http://proceedings.mlr.press/v37/martens15.html)
    
-   [https://github.com/alecwangcq/KFAC-Pytorch](https://github.com/alecwangcq/KFAC-Pytorch)
    
-   [https://paperswithcode.com/paper/optimizing-neural-networks-with-kronecker](https://paperswithcode.com/paper/optimizing-neural-networks-with-kronecker)
- 

### Blog Entries

- [Diffusion Model](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/#nice) 

#### Variational Methods
#TODO this is more general
- [Variational Bayes](https://blog.evjang.com/2016/08/variational-bayes.html)
- [Variational Lower Bounds](https://xyang35.github.io/2017/04/14/variational-lower-bound/)


#### Energy-Based Models
- [Physics of Energy-Based Models](https://towardsdatascience.com/the-physics-of-energy-based-models-1121122d0d9)
	- https://physicsofebm.github.io/

- [PyTorch implementations of Generative Adversarial Networks.](https://github.com/eriklindernoren/PyTorch-GAN)


# Score Based Generative Models

https://yang-song.github.io/blog/2021/score/
- [Estimation of Non-Normalized Statistical Models by Score Matching](https://www.jmlr.org/papers/v6/hyvarinen05a.html)
    
-   score based models and DDBM
-   https://yang-song.github.io/blog/2021/score/