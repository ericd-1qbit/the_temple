\subsection{PCA - Principal Component Analysis}

  

%https://towardsdatascience.com/a-one-stop-shop-for-principal-component-analysis-5582fb7e0a9c

\paragraph{Use Case:}

  

\begin{itemize}

  \item reduction of number of variables, without knowing which variables to completely remove

  \item ensure independence of all variables

  \item do not care about too much about interpretability of variables

\end{itemize}

  

\paragraph{Makes use of:}

\begin{itemize}

  \item measure of how each variable is associated with one another. (Covariance matrix.)

  \item directions in which our data are dispersed. (Eigenvectors.)

  \item relative importance of these different directions. (Eigenvalues.)

  \item PCA combines our predictors and allows us to drop the eigenvectors that are relatively unimportant.

\end{itemize}

  

\paragraph{Notes:}

\begin{itemize}

  \item important if many variables considered

  \item reduce dimension of feature space: \emph{dimensionality reduction}

  \item fewer correlations to consider, less overfitting

  \item dim reduction: feature \textbf{elimination} or \textbf{extraction} (PCA)

  \item construct new, independent variables from old set by combining them in specific way

  \item drop least important PC - still retain valuable info from ALL original vars

\end{itemize}