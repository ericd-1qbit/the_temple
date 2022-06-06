# Diffusion Models
Relates to: [Generative Models]()

## In short:
- Kind of generative model relying on Markov chains
- 2 steps: 
	- forward diffusion - add random noise to given data
	- reverse diffusion - reconstruct/generate data from noisy sample
![Pasted image 20220601150447.png](app://local/Users/ericdrechsler/codez/the_temple/Pasted%20image%2020220601150447.png?1654121087214)

### Forward Diffusion

1. sample datapoint from data distribution $$x_0\sim q(x)$$
2. Add Gaussian noise to the datasample in $T$ steps. $$z\sim\mathcal{N}(0,1)\rightarrow q(x_t|x_{t-1})=zq(x_{t-1})$$ #TODO verify this, this is probably not how it works
3. Produce successively noisier samples $x_0,x_1,...,x_T$ . The amount of noise added at each step is determined by variance schedule $\beta_t\in(0,1)$ . $$q(x_t|x_{t-1})=\mathcal{N}(x_t;\sqrt{1-\beta_t}x_{t-1},\beta_t)$$
4. The final noisy sample distribution is thereby given by $$q(x_{1:T}|x_0)=\prod_{t=1}^{T}{q(x_t|x_{t-1})}$$
### Reverse Diffusion
1. Reverse the diffusion steps starting from a noisy sample $$x_T\sim\mathcal{N(0,I)}$$
2. It is hard to estimate $q(x_{t-1}|x_{t})$. Find an approximate conditional distribution $$p_\theta(x_{0:T})=p(x_T)\prod_{t=1}^{T}{p_\theta(x_{t-1}|x_t)}$$ where $$p_\theta(x_{t-1}|x_t)=\mathcal{N}(x_{t-1};\mu_\theta(x_t,t),\Sigma_\theta(x_t,t))$$
3. Use the Kullback-Leibler Divergence $D_{KL}$ to quantify the distance between the approximate and actual probability distribution $$D_{KL}(q(x_{1:T}|x_0)||p_\theta(x_{1:T}|x_0)))$$
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
	- used for: object recognition, 


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