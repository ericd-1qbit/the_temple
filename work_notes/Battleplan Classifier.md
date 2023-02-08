Goal for April:

Delivering Synthetic Images to Synthesis Health. We want to be able to evaluate the quality of these images by:
- benchmarking the 


Wrap things up as we have them and provide images to SH.

- Our aim is to check if those labels are representative enough to a classifier
- predict classes of our synthetic images using pre-trained DenseNet121
- measure metrics Accuarcy, Precision, AUROC
- compare metrics to different Dataset flavours - real, synthetic, real+synthetic
- create a table to show some statistic on the classifier performance on different classes
  
Asses the quality of the synthetic images via  
1- training a classier on combination of real/synthetic images, and,  
2- investigating the potential improvement in the classier performance through metrics such as Accuarcy, Precision, AUROC, and,  
3- generate statistics to quantify the performance of variant setting of the data size and combinations (R/S) of data for the chosen classes.


Strategies:  
1- Develop the training pipeline for the real dataset. 
This includes data pipeline (train/val/test), model pipeline, and evaluation (metrics) pipeline.  
2- Test the pipeline for the real dataset. Normal vs. Abnormal classes.  
3- Extend the pipeline to the synthetic dataset. The same components as above.  
4- Test the pipeline for simple case, Normal vs. Abnormal classes.  
5- Create a benchmark plan based on other works and RoentGen work. This benchmark plan should focus on one short term and one long term plan. Short term, to show the model works well on Soft Mass Tissue label, this is the label of interest by SH. The long term includes statistics that we might need in the future in case of producing a manuscript of this work.

- start by predicting labels with the existing DenseNet121 on the real dataset to confirm we implement things properly
- then compare performances on real, synthetic and augmented datasets by evaluating Accuracy, Precision, AUROC
- then train the DenseNet121 and see whether performance changes as is done in the RoentGen table on that page

- pre-trained model on the PadChest data: data+labels that we generated the synthetic images FROM, then we cannot use that model as the data has already leaked into that model
- either should re-train this model based on a proper train/test and follow the same approach on synthetic data

- classify real images using pre-trained DenseNet
- re-train the network on synthetic+real data