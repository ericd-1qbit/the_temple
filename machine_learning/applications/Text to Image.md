# Text-to-Image: Diffusion, Text Conditioning, Guidance, Latent Space

https://eugeneyan.com/writing/text-to-image/

- 2021-2022:
	- rapid development in text to image models:
		- DALL-E, DALL-E 2, Imagen, Stable Diffusion
## **Diffusion**: 
*- add Gaussian noise to data gradually and learn how to re-generate original input*

- first paper **“[Deep Unsupervised Learning using Nonequilibrium Thermodynamics](https://arxiv.org/abs/1503.03585)**, by Sohl-Dickstein in 2015.
	- A central problem in machine learning involves modeling complex data-sets using highly flexible families of probability distributions in which learning, sampling, inference, and evaluation are still analytically or computationally tractable. Here, we develop an approach that simultaneously achieves both flexibility and tractability. The essential idea, inspired by non-equilibrium statistical physics, is to systematically and slowly destroy structure in a data distribution through an iterative forward diffusion process. We then learn a reverse diffusion process that restores structure in data, yielding a highly flexible and tractable generative model of the data. This approach allows us to rapidly learn, sample from, and evaluate probabilities in deep generative models with thousands of layers or time steps, as well as to compute conditional and posterior probabilities under the learned model.
	- Inspired by non-equilibrium thermodynamics
	- key advantage: provides a generic model to describe complex data which is both flexible AND tractable
	- key idea: systematically, slowly destroy structures in data and learn how to reconstruct them in an incremental manner, each small step retaining tractability
		- forward diffusion: Markov chain, progressively adding noise
		- reverse diffusion: diffusion probabilistic model

Stochastic Drift Term:
	- the expectation 'drifts' toward a value that gets larger and larger (assuming 𝜇μ is positive).


- **[Denoising Diffusion Probabilistic Models (DDPM; 2020)](https://arxiv.org/abs/2006.11239)**
	- Forward diffusion (q) is a predefined process that gradually adds Gaussian noise to the image until it’s pure noise. Reverse diffusion (p) is a learned process that gradually denoises an image starting from pure noise until we get an actual image.
	- ![[Pasted image 20230123160711.png]]

- p(xt-1|x_t) is intractable. It would need the distribution of all possible images to calculate the probability. 
	- instead: use a parameterised neural network to learn the distributions
- As the forward process noise is Gaussian, let's assume the reverse process is too - express the reverse probability distributions as Gaussians with mean and variance

In layman’s terms, the probability of the less noisy image () given a noisier image () from the previous timestep () is drawn from a Gaussian distribution () where the mean is the mean of  at timestep  and the variance is the variance of  at timestep . Thus, the neural network needs to learn the mean () and variance (). That said, in DDPM, the variance is predefined and the network only has to learn the mean.

![[Pasted image 20230123161858.png]]

Line 1: Start while loop
Line 2: Sample a random clean image () from the set of images
Line 3: Sample a noise level () uniformly from 1 to max 
Line 4: Sample some noise () from a Gaussian and corrupt image with the noise
Line 5: Train the neural network to predict the noise based on the corrupted image
Line 6: End while loop when model converges

![[Pasted image 20230123161918.png]]
-   Line 1: Get a sample noise image (xT) from a Gaussian distribution
-   Line 2: Iterate from timestep T to timestep 1
-   Line 3: Sample additional Gaussian noise (z if timestep > 1 else zero, because we just return the clean image at timestep 1)
-   Line 4: Get the slightly denoised image (xt−1) by subtracting the noise (ϵθ(xt,t)) from the noisy image (xt), and then adding back some noise (z)
-   Line 5: End iteration
-   Line 6: Return clean image from timestep 1


## **Text conditioning**: 
- given a text prompt, generate specific image

- good entry point; **[Contrastive Language-Image Pre-training (CLIP; 2021)](https://arxiv.org/abs/2103.00020)**
	- 

## **Classifier guidance**: 
	- "Using classifier gradients to text-increase image alignment" TODO

## **Latent space** 
- embedd images in a lower-dimensional space and run diffusion process in that space
- See #stablediffusion