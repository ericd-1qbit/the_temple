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

##### Torch
Input:
$$(N,C_{in},H_{in},W_{in})$$
Output: $$(N,C_{out},H_{out},W_{out})$$
$$H_{out}=(H_{in}-1)s_0-2p_0+d_0(k_0-1)+p^{out}_0+1$$
$$W_{out}=(W_{in}-1)s_1-2p_1+d_1(k_1-1)+p^{out}_1+1$$
with
- $s_{0/1}$: stride
- $p_{0/1}$: padding
- $k_{0/1}$: kernel size
- $p^{out}_{0/1}$: output padding
