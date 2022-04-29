\subsection{Linear Regression}

  

\paragraph{Regression}

\begin{itemize}

  \item modelling target value given independent (from each other) predictors

  \item used in forecasting/cause and effect analyses between variables

  \item find exact relationship between independent variable set x and dependent variable y

\end{itemize}

\paragraph{Linear Regression}

\begin{itemize}

  \item relationship in question is linear

  \item relies on \textbf{cost function}

  \item measures difference between prediction and actual value y

  \item goal: find minimum of this cost function

  \item minimisation procedure: \emph{gradient descent} - update parameters iteratively

  \item stepwise approach minimum - number of steps corresponds to learning rate

  \item using partial derivatives to calculate updated parameters, eg. for parameters $a,b$ and learning

 rate $\alpha$:

\end{itemize}

\begin{align}

  a&=a-\alpha\frac{\delta J}{\delta a}\\

  b&=b-\alpha\frac{\delta J}{\delta b}\\

\end{align}

\paragraph{Logistics Regression}

\begin{itemize}

  \item relationship in question is linear

  \item relies on \textbf{cost function}

  \item measures difference between prediction and actual value y

  \item goal: find minimum of this cost function

  \item minimisation procedure: \emph{gradient descent} - update parameters iteratively

  \item stepwise approach minimum - number of steps corresponds to learning rate

  \item using partial derivatives to calculate updated parameters, eg. for parameters $a,b$ and learning

 rate $\alpha$:

\end{itemize}

\begin{align}

  a&=a-\alpha\frac{\delta J}{\delta a}\\

  b&=b-\alpha\frac{\delta J}{\delta b}\\

\end{align}