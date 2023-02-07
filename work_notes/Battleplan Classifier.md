-   _**Convince ourselves that the generated images are valuable.**_
    
-   predict classes of our synthetic images using pre-trained DenseNet121 if possible
    
-   measure metrics Accuarcy, Precision, AUROC
    
-   compare metrics to different Dataset flavours - real, synthetic, real+synthetic
    
-   Reproduce a version of this table from the RoentGen paper
    For the goal part, let’s be more quantitative to ensure which part are we focusing.  

Here is my suggestions:  
1- We can remove the first goal as it is vague and genetic.  
2- I don’t think the second goal is what we aim to do here. This goal will be indirectly achieved when we are training and predicting on samples. Maybe a bit misleading. Basically we usually take the labels from conditioned model, Our aim is to check if those labels are representative enough to a classier or nor?  
3- Last goal. I am not sure if we can go ahead with this goal. RoentGen works based on MIMIC dataset, which is not the same as ours. Maybe one thing we can focus is to have a Table to show some statistic on the classifier performance on different classes.I like to suggest the following goal for this part of the work:Asses the quality of the synthetic images via  
1- training a classier on combination of real/synthetic images, and,  
2- investigating the potential improvement in the classier performance through metrics such as Accuarcy, Precision, AUROC, and,  
3- generate statistics to quantify the performance of variant setting of the data size and combinations (R/S) of data for the chosen classes.Strategies:  
1- Develop the training pipeline for the real dataset. This includes data pipeline (train/val/test), model pipeline, and evaluation (metrics) pipeline.  
2- Test the pipeline for the real dataset. Normal vs. Abnormal classes.  
3- Extend the pipeline to the synthetic dataset. The same components as above.  
4- Test the pipeline for simple case, Normal vs. Abnormal classes.  
5- Create a benchmark plan based on other works and RoentGen work. This benchmark plan should focus on one short term and one long term plan. Short term, to show the model works well on Soft Mass Tissue label, this is the label of interest by SH. The long term includes statistics that we might need in the future in case of producing a manuscript of this work.