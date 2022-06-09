# Image Segmentation
### Task:
- assign each pixel in image a label to classify if pixel belongs to specific class
- used for: 
	- object recognition
	- occlusion boundary estimation
	- image compression/editing
### Architectures
- fully [[CNN]]
- encoder-decoder with skip connections
- [[UNET]]
- transformer based architecture
- diffusion based image segmentation model
	- Diffusion Model with Unet architecture - incrementally improve generation
	- conditioning of input image: generation of another encoding path; similar to conventional Unet encoder-decoder use
	- merging of two encoder paths


### Method:
- Diffusion method for image segmentation (Tomer et al., 2021)
### Datasets
Cityscape, Vaihingen, MoNuSeg
### Benchmarks
Google open images, SYNTHIA


