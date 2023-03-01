Guys, super-duper preliminary news, but really exciting, so I thought I’d share:

We can successfully run the classifier for eval purposes on real, synthetic and augmented datasets now! 

When evaluating metrics on these 3 scenarios, we get these numbers (for 576 real samples and the 5500 synthetic images):

Real DS
{'accuracy': tensor(0.0895),
 'auroc': tensor(0.2393),
 'precision': tensor(0.0895)}

Synthetic DS
{'accuracy': tensor(0.2072),
 'auroc': tensor(0.4440),
 'precision': tensor(0.2072)}

Augmented DS
{'accuracy': tensor(0.1954),
 'auroc': tensor(0.4235),
 'precision': tensor(0.1954)}

Many caveats in these numbers, but the general message is pretty evident: The