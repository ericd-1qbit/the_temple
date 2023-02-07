- Our aim is to check if those labels are representative enough to a classifier
- predict classes of our synthetic images using pre-trained DenseNet121
- measure metrics Accuarcy, Precision, AUROC
- compare metrics to different Dataset flavours - real, synthetic, real+synthetic
- ROentGen paper 
- Table to show some statistic on the classifier performance on different classes

3- Last goal. I am not sure if we can go ahead with this goal. RoentGen works based on MIMIC dataset, which is not the same as ours. Maybe one thing we can focus is to have a Table to show some statistic on the classifier performance on different classes.I like to suggest the following goal for this part of the work:Asses the quality of the synthetic images via  
1- training a classier on combination of real/synthetic images, and,  
2- investigating the potential improvement in the classier performance through metrics such as Accuarcy, Precision, AUROC, and,  
3- generate statistics to quantify the performance of variant setting of the data size and combinations (R/S) of data for the chosen classes.Strategies:  
1- Develop the training pipeline for the real dataset. This includes data pipeline (train/val/test), model pipeline, and evaluation (metrics) pipeline.  
2- Test the pipeline for the real dataset. Normal vs. Abnormal classes.  
3- Extend the pipeline to the synthetic dataset. The same components as above.  
4- Test the pipeline for simple case, Normal vs. Abnormal classes.  
5- Create a benchmark plan based on other works and RoentGen work. This benchmark plan should focus on one short term and one long term plan. Short term, to show the model works well on Soft Mass Tissue label, this is the label of interest by SH. The long term includes statistics that we might need in the future in case of producing a manuscript of this work.



-   I think the first goal sets the stage for what we want to do with this for now, or? Convincing ourselves that we produce conditioned images for each class a classifier can pick up so we can share them with SH? That would entail a different approach than let’s say “Beat paper XYZ in metric ABC”…
-   Do you think we need to set up a sophisticated training pipeline (train/val/test) to start with? Ideally, we don’t need to train DenseNet121. That is what was done in the RoentGen paper, they took the pre-trained version to calculate their metrics.
-   What do you think is the simplest possible goal to start with? I thought it would be good to

-   predict labels with the existing DenseNet121 on the real dataset to confirm we implement things properly
-   then compare performances on real, synthetic and augmented datasets by evaluating Accuracy, Precision, AUROC
-   then train the DenseNet121 and see whether performance changes as is done in the RoentGen table on that page (yes, for a different dataset).

Thanks Eric. I believe we are converging on this. Usually I see goal as a problem statement without referring to solution or tools. Strategies are solution and tools. If the goal in the page are technical necessity then let's clarify them further and have them as solution, strategies.

-   By training pipeline I mostly mean the training model. If it is a pre-trained model then that is even better. What I wrote is generic.
-   If we want to go with pre-trained model then the we should be very careful with a pre-trained model on the PadChest data. If the model already has seen the data+labels that we generated the synthetic images FROM, then we cannot use that model as the data has already leaked into that model. I had this in mind when considering this. I believe we either should re-train this model based on a proper train/test and follow the same approach on synthetic data, or pick-up the pre-trained model from one dataset and generate the synthetic data from another dataset to do a proper comparison here. This is basically the idea behind train/val/test.
-   I believe a combination of these suggestion should give you a better idea on how to create the page as well as different milestone for this task.


Quoting from the Roentgen work "_we measure a 5% improvement of a classifier trained jointly on synthetic and real images, and a 3% improvement when trained on a larger but purely synthetic training set._". They do re-train the network on synthetic+real data. Otherwise things are really not that meaningful, i.e., using a pre-trained network for assessing the accuracy of the classifier.  
More on this tomorrow.

That’s true Ehsan, this is for the augmented dataset measurements. Table 3 in the paper, they evaluate models trained on real data and I quote

> Without being further modification, a pre-trained classifi- cation model (DenseNet-121, XRV) was used to classify both the real images (the p19 test set baseline) as well as 5,000 images (one image per prompt) per fine-tuned SD model.

That could be our first step, I’ll consider it in our battleplan. 

I would like to talk about this as I don’t understand their logic why such an approach is reasonable. Not that they are wrong but I don’t understand it and maybe there is a tiny chance they are not being rigorous in their benchmark setting.