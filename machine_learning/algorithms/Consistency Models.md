
Here is a summary of yesterday's discussion of Consistency models  [https://arxiv.org/abs/2303.01469](https://arxiv.org/abs/2303.01469)  

-   Motivated by slow generation for diffusion models (10 to 1000 model evaluation)
-   Instead of learning reverse-time SDE `f(x_{t},t) = x_{t-1}`, learns to map any `x_{t}` to the data `x_{0}`, thus generating in a single step `f(x_{t},t) = x_{0}`.
-   Still possible to tradeoff quality for more compute by re-noising and de-noising in alternance.
-   Two training options: (i) distilling (learning from pre-trained diffusion models) or (ii) standalone.
-   Distilling leads to new SOTA FID for single-step generation CIFAR-10 and ImageNet.
-   Standalone outperform all non-adversarial single-step models (i.e. do not beat GANs).

Worth noting:  

-   They preferred "EDM" for all pre-trained diffusion models [https://arxiv.org/pdf/2206.00364.pdf](https://arxiv.org/pdf/2206.00364.pdf)
-   Their loss depends on a distance function, and they found that "LPIPS" to outperform L2 and L1 metrics in [https://arxiv.org/pdf/1801.03924.pdf](https://arxiv.org/pdf/1801.03924.pdf)
-   In addition to FID and IS, they use precision and recall to evaluate the generative models as presented in [https://arxiv.org/pdf/1904.06991.pdf](https://arxiv.org/pdf/1904.06991.pdf)
-   Training relies heavily on the exponential moving average (EMA) of the weights (this is where "stopgrad" is used)

Something I forgot yesterday:  

-   architecture is the same as in previous score models `s(x,t)`, but they need a time-dependant skip connection `f(x,t) = c_in(t) x + c_out(t) * s(x,t)` to ensure that `f(x_0,0) = x_0`.


For those who are new to diffusion models, here are papers we talk about most often:  

-   Original diffusion idea (Sohl-Dickstein, 2015) : [http://arxiv.org/abs/1503.03585](http://arxiv.org/abs/1503.03585)
-   Similar score-matching idea (Song, 2019): [http://arxiv.org/abs/1907.05600](http://arxiv.org/abs/1907.05600)
-   **NCSN**, score-matching rivalling GANs  (Song, 2019): [http://arxiv.org/abs/2006.09011](http://arxiv.org/abs/2006.09011)
-   **DDPM**, diffusion beating GANs (Ho, 2020): [http://arxiv.org/abs/2006.11239](http://arxiv.org/abs/2006.11239)
-   Fine-tuning (Nichol & Dhariwal, 2021) [http://arxiv.org/abs/2102.09672](http://arxiv.org/abs/2102.09672)
-   **Unifying** DDPM, NCSN, SDEs and ODEs (Song, 2021) [http://arxiv.org/abs/2011.13456](http://arxiv.org/abs/2011.13456)
-   More fine-tuning (Karras, 2022) [http://arxiv.org/abs/2206.00364](http://arxiv.org/abs/2206.00364)
-   Cold diffusion: diffusion is not needed (Bansal 2022) [http://arxiv.org/abs/2208.09392](http://arxiv.org/abs/2208.09392)

Let me know if you think I miss some.