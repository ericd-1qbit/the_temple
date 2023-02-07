# Questions & Answers

## Why is the Diffusion step used on the latent space? What is the difference between $z_0$ and the noisy $z_T$? 
How are structures embedded in $z_0$ and what does the addition of noise do to the latent vector? 
Why is Diffusion needed at all? 
Why are the output images not blurry?
Does the DM add some kind of detail to the 


A Variational Autoencoder consists of:

- true posterior distribution $p_\theta(z|x)$ which is modelled by the approximate posterior distribution $q_\phi(z|x)$ (the encoder network)
- a prior $p(z)$ 
- the conditional likelihood distribution $p_\theta(x|z)$ (the decoder network)

The goal of training the VAE is to minimise reconstruction loss, while on the same hand ensuring that the approximate posterior distribution stays as simple as possible (the authors in the LDM paper call this "avoiding high variance latent spaces"). The following expression is the objective of a VAE training:

$${\cal L}\left( {x,\hat x} \right) + KL\left( {q_{\phi}\left( {z|x} \right)||p\left( z \right)} \right)
$$

In the Vanilla-VAE, the approximate posterior $q_\phi(z|x)$  is modelled using Gaussians with mean $\mu$ an variance $\sigma$ which are the learned output of the encoder. $P(z)$ is the "simple" distribution the appr. posterior is regularised to, eg. a standard Gaussian $\mathcal{N}(0,1)$. (Sidenote: The LDM paper tests another regularisation too - vector quantisation).
In a Vanilla VAE one would then go ahead and sample $z\sim\mathcal{N}(0,1)$, feed that random noise through the decoder and obtain a synthetic sample.

The deal with the LDM approach is, that they DO NO sample $z\sim\mathcal{N}(0,1)$ but they sample

$$
z=\mathcal{E}_\mu(x)+\mathcal{E}_\sigma(x)*\varepsilon
$$

$\mathcal{E}_\mu$, $\mathcal{E}_\sigma$ are the encoder outputs of the learned


The information about the input data is stored in the parameters of the encoder and decoder and in the values in the latent space.

The sample can be obtained by sampling from the Gaussian distribution that is defined by the mean and variance values output by the encoder network for a given input. The sample from the latent space is then passed through the decoder network to generate the output, which is a reconstruction of the input data.

From the paper:

Because our subsequent DM is designed to work with the two-dimensional structure of our learned latent space z = E(x), we can use relatively mild compres- sion rates and achieve very good reconstructions. This is in contrast to previous works [23, 66], which relied on an arbitrary 1D ordering of the learned space z to model its distribution autoregressively and thereby ignored much of the inherent structure of z.
ence, our compression model preserves details of x better (see Tab. 8). 

The full objective and training details can be found in the supplement.

![[Pasted image 20230206154611.png]]


## Explain how the cross-attention mechanism inside the LDM works. What is the "switch"?