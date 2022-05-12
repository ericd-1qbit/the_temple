# Linear Regression

## Regression

- modelling target value given independent (from each other) predictors

- used in forecasting/cause and effect analyses between variables

- find exact relationship between independent variable set x and dependent variable y



### Linear Regression

- relationship in question is linear

- relies on \textbf{cost function}

- measures difference between prediction and actual value y

- goal: find minimum of this cost function

- minimisation procedure: \emph{gradient descent} - update parameters iteratively

- stepwise approach minimum - number of steps corresponds to learning rate

- using partial derivatives to calculate updated parameters, eg. for parameters $a,b$ and learning

 rate $\alpha$:


$$
\begin{align}

  a&=a-\alpha\frac{\delta J}{\delta a}\\

  b&=b-\alpha\frac{\delta J}{\delta b}\\

\end{align}
$$

### Logistics Regression