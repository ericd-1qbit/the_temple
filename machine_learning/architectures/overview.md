\paragraph{Statistical Inference}

is the process of finding properties of a dataset by performing data analysis 

and understanding the characteristics of the underlying probability distribution 

the data is following.

  

\paragraph{Bayesian Inference} is a form of statistical inference. Properties are deducted from a dataset. 

Update the model as more information becomes available following Bayes Theorem.

  

$$

P(\theta|x)=\frac{P(x|\theta)P(\theta)}{P(x)}    

$$

  

Terminology:

$P(\theta)$ is the \textbf{Prior}. Represents our "beliefs" of the true value of the model parameters.

$P(\theta|x)$ is the \textbf{Posterior}. It represents the beliefs after having evaluated the data.

$P(x|\theta)$ is the \textbf{Likelihood}. How likely does our model reflect the data?

  

Therefore we can calculate the posterior distribution using our prior beliefs and updating the likelihood. 

  

  

  

  

\section{Bump hunts}

  

\subsection{(Un-) Conditional Fit}

An uncoditional macimum likelihood estimator (MLE) provides the best fit results

for a given set of parameters, including the free floating Parameters of

interest (POI). Concrete example: all nuissance parameters and signal strength are

floating, unconditional MLE is best result of adjusting model to data.

A conditional MLE is the best fit result when a POI is fixed to a certain value.

In the example, the siugnal strength is fixed at a value and NPs are estimated

for the best fit result.