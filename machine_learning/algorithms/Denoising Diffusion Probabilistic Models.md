# Denoising Diffusion Probabilistic Models

https://arxiv.org/abs/2006.11239

![[Pasted image 20220601154435.png]]

We use a U-Net with self-attention;


To represent the reverse process, we use a U-Net backbone similar to an unmasked PixelCNN++ [52, 48] with group normalization throughout [66]. Parameters are shared across time, which is specified to the network using the Transformer sinusoidal position embedding [60]. We use self-attention at the 16 × 16 feature map resolution [63, 60]. Details are in Appendix B.

Our neural network architecture follows the backbone of PixelCNN++ [52], which is a U-Net [48] based on a Wide ResNet [72]. We replaced weight normalization [49] with group normalization [66] to make the implementation simpler. Our 32 × 32 models use four feature map resolutions (32 × 32 to 4 × 4), and our 256 × 256 models use six. All models have two convolutional residual blocks per resolution level and self-attention blocks at the 16 × 16 resolution between the convolutional blocks [6]. Diffusion time t is specified by adding the Transformer sinusoidal position embedding [60] into each residual block. Our CIFAR10 model has 35.7 million parameters, and our LSUN and CelebA-HQ models have 114 million parameters. We also trained a larger variant of the LSUN Bedroom model with approximately 256 million parameters by increasing filter count.



# HIL meeting 22 06 22
YOUR CLASSIFIER IS SECRETLY AN ENERGY BASED MODEL AND YOU SHOULD TREAT IT LIKE ONE
https://arxiv.org/pdf/1912.03263.pdf


- not a state of the art paper, but nice ideas
- fid-score is the main metric
- idea: 
	- train EBM classifier
	- allow classifier to be robust against adversarial attacks
	- imrpove classifier
	- generative model as well
- work done by jeff in the past is on confluence
- Langevin sampling or SGLD
- either maximise log(p(x,y)) or log p(x)
	- this correpsonds to maximising the probabiloity over the dataset, eg. making the model express the dataset probability distribtuioon best
- confidence metric
- what is "calibrated"?
	- NN output - should correpsond to real world output
	- calibration is a measure of hacving good representation
	- if NN is too confident at predicting wrong things and low confident on correct predictions - adjust this!
	- 