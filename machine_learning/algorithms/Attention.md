# Attention

https://towardsdatascience.com/matters-of-attention-what-is-attention-and-how-to-compute-attention-in-a-transformer-model-4cbbd3250307

attention is a concept borrowed from human cognition
- efficient use of resources
- facilitates the semantic understanding of raw sensory data
- the ability to register the environmental stimuli by processing and saving it in memory for future recall
- Visual Attention is a process of identifying salient objects/regions in the scene and registering them as potential meaningful stimulus helpful in achieving the goal
-  this is done in stages, each stage registering different feature levels of salient (important) objects
	- from low level - orientation, motion, color, intensity 
	- to high level - details of an object, eyes in a face etc.
	- these are summarised into an abstract representation - the **saliency map**
- same holds for text attention - building a saliency map of the most descriptive words in a given text.

## Attention in Transformers

Sequence modelling:
- represent an input sequence - eg. words
- recover another sequence which semantically maps to the input
- long been modelled using RNNs, as they can capture semantic relationships between elements of the sequences
	- disfavoured now, as overcomplicated - high training, mediocre performance
- Transformers were proposed as a remedy, and they quickly became a standard way to build language models due to their relative efficiency and accuracy

**Self-attention**
- represent the intra relationship of positions of various elements in a sequence to model
Transformers use self-attention mechanism alone in order to represent & map the input and output sequences

**Vector Embedding** 
- map input sequences to hyperspace
- cluster similar words  

**Position Embedding**
- embed the position of a given word for semantic context
- use sinusoidal position embedding to reduce memory requirements

**Input embeddings to Transformer:**
- Combined representation: add vector + position embedding

#### attention creates the semantic power of a transformer
- allows to determine the most salient words and inter-relationship in a sequence
- depends on:
	- Q - QUERY
	- K - KEY
	- V - VALUE
- 