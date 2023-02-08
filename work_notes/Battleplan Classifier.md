Goal for April:

Delivering Synthetic Images to Synthesis Health. 

We want to be able to assess the quality of these images by:
- calculating FID-scores and MS-SSIM metrics on synthetic image datasets generated with NCSN and DDPM models 
- study whether the augmentation of real datasets with synthetic images improves classifier performance on predicting pathology classes as measured by the metrics Precision, Accuarcy


Milestones
	
	- Calculate Precision and Accuarcy on class predicition for real dataset using the pre-trained DenseNet classifier. 
		- This is a proof-of-concept end-to-end example which will show us to what extend we can use the pre-trained classifier 
	- Develop a training pipeline for the DenseNet classifier on the real dataset and train for the "soft tissue mass" (STM) label.
		- The STM label is not part of the pre-trained densenet classes.
	- Add testing infrastructure to pipeline, where Precision and Accuarcy are calculated on a re-trained Densenet classifier on the various dataset flavours. 
	- Add data-infrastructure for synthetic and augmented dataset to the training pipeline.
	- Run a benchmark to create a summary statistics of dataset variants vs Metrics Precision, Accuracy for the STM label.