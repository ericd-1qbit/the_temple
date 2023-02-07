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
1- Develop the training pipeline for the real dataset. This includes data pipeline (train/val/test), model pipeline, and evaluation (metrics) pipeline.  
2- Test the pipeline for the real dataset. Normal vs. Abnormal classes.  
3- Extend the pipeline to the synthetic dataset. The same components as above.  
4- Test the pipeline for simple case, Normal vs. Abnormal classes.  
5- Create a benchmark plan based on other works and RoentGen work. This benchmark plan should focus on one short term and one long term plan. Short term, to show the model works well on Soft Mass Tissue label, this is the label of interest by SH. The long term includes statistics that we might need in the future in case of producing a manuscript of this work.

-   Do you think we need to set up a sophisticated training pipeline (train/val/test) to start with? Ideally, we don’t need to train DenseNet121. That is what was done in the RoentGen paper, they took the pre-trained version to calculate their metrics.
-   What do you think is the simplest possible goal to start with? I thought it would be good to
-   predict labels with the existing DenseNet121 on the real dataset to confirm we implement things properly
-   then compare performances on real, synthetic and augmented datasets by evaluating Accuracy, Precision, AUROC
-   then train the DenseNet121 and see whether performance changes as is done in the RoentGen table on that page (yes, for a different dataset).

-   If we want to go with pre-trained model then the we should be very careful with a pre-trained model on the PadChest data. If the model already has seen the data+labels that we generated the synthetic images FROM, then we cannot use that model as the data has already leaked into that model.
- I had this in mind when considering this. I believe we either should re-train this model based on a proper train/test and follow the same approach on synthetic data, or pick-up the pre-trained model from one dataset and generate the synthetic data from another dataset to do a proper comparison here. This is basically the idea behind train/val/test.


- classify real images using pre-trained DenseNet
- re-train the network on synthetic+real data