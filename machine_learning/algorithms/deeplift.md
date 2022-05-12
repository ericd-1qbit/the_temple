# DeepLift - Learning Important Features through propagation of activation differences

Reading arXiv:1704.02685v2

## Summary
- provide interpretability of NN output

- associate output to input features by backproping through all neurons 

- contribution scores of each neuron by comparing activation of n to a reference 

## Other Methods
- Perturbation-based fwd prop approach: Observe impact on output after perturbing input or neurons

 Problem here is that once input contribution has saturated the impact on output, impact of input on importance not attributed any further.
  Also computationally expensive due to additional fwd prop. 
- Guided backpropagation - Combination of Gradients and deconvolutional networks. Saliency Maps
- Gradient x Input - elementwise product. layerwise relevance propagation
- integrated gradients
- grad/guided CAM
  

## DeepLIFT
Compute a contribution score for a given neuron $x$ to the output $t$.

## Summation-To-Delta
The contribution score is defined such that a summation over all changes from ref in a given layer of n neurons results is the change from ref in the target neuron.


### Chain Rule for Multipliers

Multipliers qunatify the contribution of the change in neuron x to the target change t. 

Similar to partial derivatives. For an additional layer, the Multipliers 

propagate from one layer to the next. Like chain rule - allows to apply backprop.

### Defining a reference

Problem dependent. Differences measured against what? 

  

### Separating Positive And Negative contributions

  

### Contribution Score Assignment rules

- Linear 
- Rescale
- RevealCancel

### Target Layer Choice and Softmax
  

## Claimed Advantages

- zero gradients still allow for propagation of importance score
- avoid discontinuity artifacts in gradient calculations
- positive and negative contributions to importance separated - reveal dependencies missed by other methods 
