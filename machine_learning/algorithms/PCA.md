# PCA - Principal Component Analysis

%https://towardsdatascience.com/a-one-stop-shop-for-principal-component-analysis-5582fb7e0a9c

#### Use Case

- reduction of number of variables, without knowing which variables to completely remove
- ensure independence of all variables
- do not care about too much about interpretability of variables

#### Makes use of

- measure of how each variable is associated with one another. (Covariance matrix.)
- directions in which our data are dispersed. (Eigenvectors.)
- relative importance of these different directions. (Eigenvalues.)
- PCA combines our predictors and allows us to drop the eigenvectors that are relatively unimportant.


#### Notes

- important if many variables considered
- reduce dimension of feature space: \emph{dimensionality reduction}
- fewer correlations to consider, less overfitting
- dim reduction: feature \textbf{elimination} or \textbf{extraction} (PCA)
- construct new, independent variables from old set by combining them in specific way
- drop least important PC - still retain valuable info from ALL original vars

