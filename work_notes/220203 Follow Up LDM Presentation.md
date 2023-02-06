# Questions & Answers

Why is the Diffusion step used on the latent space? What is the difference between $z_0$ and the noisy $z_T$? 
How are structures embedded in $z_0$ and what does the addition of noise do to the latent vector? 
Why is Diffusion needed at all? 
Why are the output images not blurry?
Does the DM add some kind of detail to the 


From the paper:
In order to avoid arbitrarily high-variance latent spaces, we experiment with two different kinds of regularizations. The first variant, KL-reg., imposes a slight KL-penalty to- wards a standard normal on the learned latent, similar to a VAE [46, 69], whereas VQ-reg. uses a vector quantization layer [96] within the decoder. This model can be interpreted as a VQGAN [23] but with the quantization layer absorbed by the decoder. Because our subsequent DM is designed to work with the two-dimensional structure of our learned latent space z = E(x), we can use relatively mild compres- sion rates and achieve very good reconstructions. This is in contrast to previous works [23, 66], which relied on an arbitrary 1D ordering of the learned space z to model its distribution autoregressively and thereby ignored much of the inherent structure of z. Hence, our compression model preserves details of x better (see Tab. 8). The full objective and training details can be found in the supplement.




Explain how the cross-attention mechanism inside the LDM works. What is the "switch"?