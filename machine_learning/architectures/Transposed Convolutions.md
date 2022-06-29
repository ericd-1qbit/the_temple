#upsampling


#### Upsampling
If the output of a netowrk is not only a classifier but for example a full image, there's a need to increase the low-dimensional representation (after convolutions) to a high-dimensional output. The convolutions are great at focussing on _what_ is in the image but not at _where_ something is.

Upsampling methods: bi-linear/cubic interpolation, nearest neighbour, unpooling, transposed convolution.

# Transposed Convolution 
Also called 

Deconvolution
Fractionally strided convolution.

Method to perform upsampling of an image with learnable parameters.

- upsampling without pre-defined interpolation method
- Core idea:
	- learn how to reverse a convolution
	- associate one value with many others 
	- Express convolution operation as matrix
	- transpose this matrix