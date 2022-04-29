# Overview

-   [Overview](https://www.cs.ubc.ca/~schmidtm/Courses/LecturesOnML/overview.pdf)

### Machine Learning

\subsection{Formal Definition}

A formal definition given by Mitchel (1997) [56] 

\begin{quote}

  A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, 

  if the performance at tasks in T , as measured by P, improves with E.

\end{quote}

\subsection{Types of ML}

One can distinguish three different types of ML approaches, defined by the kind of input

provided to the algorithm.

\paragraph{Supervised} Learning tasks learn from labelled examples, i.e. a training dataset with 

data points $x$ and labels $y$.

\paragraph{Unsupervised} Learning tasks try to learn the underlying structure in a training data set without 

being provided specific labelling. The boundaries to supervised learning are blurry, one can transform 

an unsupervised task into a supervised one. One could marginalise over data features and do a supervised 

learning for the given feature. %TODO

$$

P(x)=\prod_{i=1}^mP(x_i|x_1,\ldots,x_{i-1})

$$

  

\paragraph{Reinforcement} learning does not rely on any dataset. The algorithm generates it's own data and 

updates the generative process according to a rules/reward functions.

  

\subsection{Important Definitions}

\begin{table}

  \begin{tabular}{r|l}

  Phrase & Explanation\\\hline

  Generalisation & Ability of an algorithm to perform on an unseen dataset.\\

  Features & Variables describing certain characteristics of the input data\\

  Feature Vector & One input data point instance\\

  train error & The error of the algorithm estimated on the training dataset.\\

  test error & The error of the algorithm estimated on the testing dataset.\\

  \end{tabular}

\end{table}

Data Mining and Machine Learning closely related

![[Pasted image 20220426084752.png]]

Deep learning is a subset of Machine Learning which is a subset of Artifical Intelligence.
![[Pasted image 20220426084859.png]]

Applications:
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

⚠️⚠️⚠️⚠️
[[Common Problems]]



[[Supervised Learning]]

[[Exploratory Data Analysis]]

[[sources]]


Machine Learning can be separated into four areas of concern:

\paragraph{Classification} tasks are mapping input data onto a discrete set of

classes by learning a function $$ h:\mathbb{R}^m\rightarrow{1,2,...,t}

$$
Canonical example is to classify dog or cat in picture.

  

\paragraph{Regression} tasks  predict a value for given input by learning a function $$

h:\mathbb{R}^m\rightarrow\mathbb{R}

$$

Canonical example is the cost of a house given various external parameters (size, location, etc).

  

\paragraph{Anomaly detection} is for identifying deviations from the bulk behaviour of data. 

Canonical example is the detection of credit card fraud.

\paragraph{Denoising} tasks take a noisy input $\tilde{x}\in\mathbb{R}^m$ and map it to noise-free data $x\in\mathbb{R}^m$ by learning the underlying features.



\begin{itemize}

  \item Which Considerations to take before translating your problem to ML?

  \begin{itemize}

    \item Does my task map to any ML paradigm?

        \item Can I write down my model analytically?

        \item What's the dimensionality of my data?

        \item data sample sizes?

  \end{itemize}

\end{itemize}




\subsection{Unsorted Notes}

\paragraph{Random}

\begin{itemize}

  \item GAN - generate Ising model

  \item translate to QA??

  \item what's a feedforward NN backpropagation?

  \item I. Goodfellow has a great many taxonomies

  \item automatic differentiation - computing derivatives with se compuhda

  \item Recurrence: The output of a layer goes back to input.

  \item Hough transform: Image analysis technique which isolates features of a particular shape in an image.

  \item Dropout of 0.2 means 20\% of nodes in a layer are deactivated randomly

\end{itemize}