\subsection{Reading arXiv:1704.02685v2 - DeepLift - Learning Important Features through propagation of a

ctivation differences}

\subsubsection{Summary}

\begin{itemize}

  \item provide interpretability of NN output

  \item associate output to input features by backproping through all neurons 

  \item contribution scores of each neuron by comparing activation of n to a reference 

\end{itemize}

\subsubsection{Previous Methods}

\begin{itemize}

  \item Perturbation-based fwd prop approach: Observe impact on output after perturbing input or neurons

.

 Problem here is that once input contribution has saturated the impact on output, impact of input on imp

ortance not attributed any further.

  Also computationally expensive due to additional fwd prop. 

 \item Guided backpropagation - Combination of Gradients and deconvolutional networks. Saliency Maps

 \item Gradient x Input - elementwise product. layerwise relevance propagation

 \item integrated gradients

 \item grad/guided CAM

\end{itemize}

  

\subsubsection{DeepLIFT}

Compute a contribution score for a given neuron $x$ to the output $t$.

  

\begin{tabular}{2}

  target neuron & t\\

  neurons or inputs & x\\

  reference value for smth & smth$^0$\\

  contribution score & $C_{\Delta x,\Delta t}$\\

  multiplier & smth$^0$\\

   & smth$^0$\\

\end{tabular}

  

\paragraph{Summation-To-Delta}

The contribution score is defined such that a summation over all changes from ref 

in a given layer of n neurons results is the change from ref in the target neuron.

  

\paragraph{Chain Rule for Multipliers}

Multipliers qunatify the contribution of the change in neuron x to the target change t. 

Similar to partial derivatives. For an additional layer, the Multipliers 

propagate from one layer to the next. Like chain rule - allows to apply backprop.

\paragraph{Defining a reference}

Problem dependent. Differences measured against what? 

  

\paragraph{Separating Positive And Negative contributions}

  

\paragraph{Contribution Score Assignment rules}

- Linear 

- Rescale

- RevealCancel

  

\paragraph{Target Layer Choice and Softmax}

  

  

\paragraph{Claimed Advantages}

\begin{itemize}

  \item zero gradients still allow for propagation of importance score

  \item avoid discontinuity artifacts in gradient calculations

  \item positive and negative contributions to importance separated - reveal dependencies missed by other methods 

\end{itemize}