# Overview

-   [Mark Schmidt Course Overview](https://www.cs.ubc.ca/~schmidtm/Courses/LecturesOnML/overview.pdf)

### Machine Learning
⚠️⚠️⚠️⚠️
[[Common Problems]]
[[Supervised Learning]]
[[Exploratory Data Analysis]]
[[sources]]

#### Formal Definition
A formal definition given by Mitchel (1997)

> A computer program is said to learn from experience $E$ with respect to some class of tasks $T$ and performance measure $P$, if the performance at tasks in $T$, as measured by $P$, improves with $E$.

Data Mining and Machine Learning closely related

![[Pasted image 20220426084752.png]]

Deep learning is a subset of Machine Learning which is a subset of Artifical Intelligence.
![[Pasted image 20220426084859.png]]


#### Types of Machine Learning algorithms 

One can distinguish three different types of ML approaches, defined by the kind of input provided to the algorithm.

- **[[Supervised Learning]]** tasks learn from labelled examples, i.e. a training dataset with data points $x$ and labels $y$.
- **[[Unsupervised Learning]]** tasks try to learn the underlying structure in a training data set without being provided specific labelling. 
	- The boundaries to supervised learning are blurry, one can transform an unsupervised task into a supervised one. One could marginalise over data features and do a supervised learning for the given feature.
$$
P(x)=\prod_{i=1}^mP(x_i|x_1,\ldots,x_{i-1})
$$
- **[[Reinforcement Learning]]** does not rely on any dataset. The algorithm generates it's own data and updates the generative process according to a rules/reward functions.

#### Types of Machine Learning problems 

- [[Classification tasks]] are mapping input data onto a discrete set of classes by learning a function $$ h:\mathbb{R^m\rightarrow{1,2,...,t}}$$
	-  Canonical example is to classify dog or cat in picture.
	
- [[Regression tasks]]  predict a value for given input by learning a function $$
h:\mathbb{R^m}\rightarrow\mathbb{R}
$$
	- Canonical example is the cost of a house given various external parameters (size, location, etc).\
	
- [[Anomaly detection]] is for identifying deviations from the bulk behaviour of data. 
	- Canonical example is the detection of credit card fraud.

- [[Denoising tasks]] take a noisy input $\tilde{x}\in\mathbb{R^m}$ and map it to noise-free data $x\in\mathbb{R^m}$ by learning the underlying features.


##### Which Considerations to take before translating your problem to ML?
1. Does my task map to any ML paradigm?
2. Can I write down my model analytically?
3. What's the dimensionality of my data?
4. What are my data sample sizes? Do I have sufficient data?

#### Applications:
- spam filtering
- credit card fraud detection
- product recommendation
- motion capture
- text recognition and machine translation
- speech recognitiojn
- face detection
- object detection
- sports analytics
- ...


## Unsorted Notes

\paragraph{Random

\begin{itemize

  \item GAN - generate Ising model

  \item translate to QA??

  \item what's a feedforward NN backpropagation?

  \item I. Goodfellow has a great many taxonomies

  \item automatic differentiation - computing derivatives with se compuhda

  \item Recurrence: The output of a layer goes back to input.

  \item Hough transform: Image analysis technique which isolates features of a particular shape in an image.

  \item Dropout of 0.2 means 20\% of nodes in a layer are deactivated randomly

\end{itemize


\paragraph{ML Overview from evernote

  

Unsupervised learning:

 - learn structure in data:

methods:

clustering

density estimation

anomaly detection

PCA  

semi-supervised: 

noisy labels

weakly supervised

  

generative models

- attempt to learn data distribution

- GANs, VAE

I. Goodfellow taxonomy


Reinforcement learning

no data!

agent to perform action on environment - receive rewards

Q_learning

DQN

SARSA

inverse reinforcement learning

Reinforcement learning: qbit ontol, jet grooming through reinforcement learning
