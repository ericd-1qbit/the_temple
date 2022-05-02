\section{Semisupervised or weakly supervised Learning}
semi-supervised: 

noisy labels

weakly supervised
  

\paragraph{Sources}

- overview: weak supervision

%https://towardsdatascience.com/non-standard-weakly-supervised-classification-problems-51b23211d4bc

%https://www.sciencedirect.com/science/article/abs/pii/S0167865515003505

  

\subsection{CWoLa - Classification without Labels}

\paragraph{Sources}

%\begin{itemize}

%  \item Presentation: {\verbatim /Users/drdre/Documents/MachineLearning/BOOST_CWoLa_Hunting.pdf}

%\end{itemize}

  

  

\paragraph{Use Case:}

\begin{itemize}

  \item extended the bump hunting with ML

  \item classification problem unknown labels or class proportions

  \item or unreliable simulations with statistical mixtures of the classes available

\end{itemize}

  

\paragraph{Makes use of:}

\begin{itemize}

  \item train directly on data

\end{itemize}

  

\paragraph{Notes}

\begin{itemize}

\item Need some variable X (e.g. mJJ) in which bg is smooth and signal is localized

\item Need some other variables {Y} (e.g. jet substructure) which may provide discriminating power which may be a-priori unknown.

\item {Y} should not be strongly correlated with X over the X-width of the signal.Or decorrelate (e.g. if we can predict or measure the correlation, that can be subtracted away to create new uncorrelated variables).

\item optimal CWola classifier same classifier as in fully-supervised ML

\item The problem of learning from unknown mixed samples can be shown to be mathematically equivalent to the problem of learning with asymmetric random label noise

\end{itemize}