evaluator configs
https://github.com/1QB-Information-Technologies/Diffusion-models/pull/639#discussion_r1046178893


double dataset_name
https://github.com/1QB-Information-Technologies/Diffusion-models/pull/639#discussion_r1046182796




https://github.com/1QB-Information-Technologies/Diffusion-models/pull/639#discussion_r1046185825
Two general comments 😊

1.  Shall we move the "datasets" directory under "src"?
2.  Shall we extract the CelebA, CIFAR10 and LSUN data sets into separate .py files as well?
3.  Please update the datasets module location in "tests/test_preprocess.py" as well

I agree with Shakib's comments.  
Adding to comment#2, also a separate .py file for `BaseDataset`


Change input_dim variable
https://github.com/1QB-Information-Technologies/Diffusion-models/pull/650#discussion_r1047844007