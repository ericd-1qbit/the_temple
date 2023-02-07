# Questions & Answers

Why is the Diffusion step used on the latent space? What is the difference between $z_0$ and the noisy $z_T$? 
How are structures embedded in $z_0$ and what does the addition of noise do to the latent vector? 
Why is Diffusion needed at all? 
Why are the output images not blurry?


A Variational Autoencoder consists of:

- true posterior distribution $p_\theta(z|x)$ which is modelled by the approximate posterior distribution $q_\phi(z|x)$ (the encoder network)
- a prior $p(z)$ 
- the conditional likelihood distribution $p_\theta(x|z)$ (the decoder network)

The goal of training the VAE is to minimise reconstruction loss, while on the same hand ensuring that the approximate posterior distribution stays as simple as possible (the authors in the LDM paper call this "avoiding high variance latent spaces"). The following expression is the objective of a VAE training:

$${\cal L}\left( {x,\hat x} \right) + KL\left( {q_{\phi}\left( {z|x} \right)||p\left( z \right)} \right)
$$

In the Vanilla-VAE, the approximate posterior $q_\phi(z|x)$  is modelled using Gaussians with mean $\mu$ an variance $\sigma$ which are the learned output of the encoder. $P(z)$ is the "simple" distribution the appr. posterior is regularised to, eg. a standard Gaussian $\mathcal{N}(0,1)$. (Sidenote: The LDM paper tests another regularisation too - vector quantisation).
In a Vanilla VAE one would then go ahead and sample $z\sim\mathcal{N}(0,1)$, feed that random noise through the decoder and obtain a synthetic sample.

The deal with the LDM approach is, that they DO NOT sample $z\sim\mathcal{N}(0,1)$ but they sample

$$
z=\mathcal{E}_\mu(x)+\mathcal{E}_\sigma(x)*\varepsilon
$$

$\mathcal{E}_\mu$, $\mathcal{E}_\sigma$ are the encoder outputs of the learned Gaussian means and variances during encoder training and $\epsilon\sim\mathcal{N}(0,1)$.

That is crucial - it means that they work with the two-dimensional output structure of the encoder. They basically sample from $q_\phi(z|x)$ instead of doing what is usually done in VAE image generation as described above. This is including much of the inherent structure of $z$. 

Furthermore during the VAE training, they weigh the regularisation very little, which ensures high-fidelity reconstructions, to quote.

They show in a table that this approach preserves the details of an input image much better during compression.

This then also explains why diffusion is relevant at all for this approach - they diffuse $z_0=\mathcal{E}_\mu(x)+\mathcal{E}_\sigma(x)*\varepsilon$  to $z_T$ , thereby adding noise to the inherent structure of z.

The conditional likelihood distribution $p_\theta(x|z)$ (the decoder network) has been trained to learn on the encoder output originally. After the Denoising Diffusion steps, that z is now slightly different, hence we get a high-fidelity but probabilistic synthetic sample. 




![[Pasted image 20230206154611.png]]


## Explain how the cross-attention mechanism inside the LDM works. What is the "switch"?