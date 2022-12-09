




https://stanfordmimi.github.io/RoentGen/



## Metrics for Medical Image Evaluation



While the general image appearance was visu- ally very similar to real CXR, some aspects like electrodes or other device components almost always contained un- realistic features (e.g. discontinuations or streaks), which made this distinction simple. In the majority of cases ra- diologists were thus able to confidently guess which image was true and which was synthetic.

## Meeting Notes:

- almost exactly what we are trying to do!
- the class conditional part we have in differs

### FID metric
- Inception is good metric for image distribution in general
	- InceptionV3 network is great for ImageNet general images
- not so great for fine features in x-ray images

Smaller FID indicates higher fidelity to the original images.
(fidelity: Genauigkeit)


### MS SSIM
- Multi-scale Structural Similarity Index Measure
https://torchmetrics.readthedocs.io/en/latest/image/multi_scale_structural_similarity.html
Smaller MS-SSIM indicates higher intra-prompt image generation diversity.
-> diversity for a given label

Goal for our metric stuff:
- maximise classifier performance
- 