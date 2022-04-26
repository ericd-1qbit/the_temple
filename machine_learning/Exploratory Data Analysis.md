# Exploratory Data Analysis
https://www.cs.ubc.ca/~schmidtm/Courses/340-F19/L2.pdf

In a nutshell:
>>Typical data mining steps: 
>> 	Involves data collection, preprocessing, analysis, and evaluation. 
>> Example-feature representation and categorical/numerical features. 
>> 	Transforming non-vector examples to vector representations. 
>> Feature transformations:
>> 	To address coupon collecting or simplify relationships between variables. 
>> Exploring data: 
>> 	Summary statistics and data visualization.
>> Supervised learning:
>> 	Using data to write a program based on input/output examples.


## Typical Data Mining Cookbook

1. Learn about the application.
2. Identify data mining task.
3. Collect data. 
4. Clean and preprocess the data. 
5. Transform data or select useful subsets.
6. Choose data mining algorithm. 
7. Data mining! 
8. Evaluate, visualize, and interpret results. 
9. Use results for profit or other goals. (often, you’ll go through cycles of the above)

## Data Types
### Categorical Data
- unordered sets:
	- Binary: yes, no
	- nominal: color

### Numerical Data
- ordered sets:
	- discrete counts: age
	- ordinal: rating
	- continuous: length

## Data Conversions
- encodings:
	- One of K/One-Hot Encoding
- text approximations:
	- bag of words 
		- replace documents with word counts
		- ignores order but captures general theme
		- compute distance between docs
- image approximations:
	- greyscale intensity
- graph approximations
	- adjacency matrix

## Data Cleaning
- Data might:
	- be noisy
	- contain outliers
	- miss values
	- have duplicated entries

## Feature Aggregation
- Combine features into new features

## Feature Selection
- remove irrelevant features

## Feature Transformation
- mathematical transformations:
	- discretisation: turn numerical data into categorical (ranges of values for example)
	- others like squares, exponentiation, logs etc.
- scaling
- fourier coefficients, spectograms, wavelets 

## Exploratory Data Analysis
- high dimensional data can be hard to inspect:
	- summary statistics
	- visualisations
	- ML+DM (? #TODO)

### Summary Statistics
 ⚠️ Can be misleading!

#### Categorical Data
- **frequencies**: number of occurences of different classes
- **mode**: category that occurs most often
- **quantiles** : categories that occur more than t times

#### Continuous Data
- location-like metrics:
	- mean: average value
	- median: half-point - 50% of data are smaller/larger
	- quantiles: a fraction k of points are larger than this value
- spread of data distributions:
	- range: [min, max]
	- variance: distance of values from mean
		- standard deviation: square root of variance
	- interquantile ranges (IQR): difference between quantiles

#### Entropy
A measure of randomness for a given dataset, related to the spread of the data distributions.
Formal definition:

>How many bits of information are encoded in the average example.

**Entropy for categorical** variable with `k` values and probability $p_c$ of value `c`:
$$H=-\sum_{c=1}^kp_c\log{p_c}$$
> **Low Entropy**: very predictable, orderly
> **High Entropy**: very random, hardly predictable

$$\begin{align}
max(H)&=\log{k}\\
min(H)&:=0
\end{align}$$

- categorical features: uniform distribution has highest entropy
- continuous features: **Normal distribution** has highest entropy ⚠️ 

#### Distances and Similarities
Summary statistics between features:
- **Hamming distance**: # elements in vector that aren't equal
- **Euclidian distance**: distance between vectors
- **Correlation**: [-1,1]
- **Rank correlation**: non-linear correlation
- **Jaccard coefficient**: distance between sets
- **Edit distance**: distance between strings 

### Visualisation
⚠️ Can be misleading. Check in particular axes and feature that is plotted.

2d plots of data can reveal many characteristics of a dataset:
- patterns, trends, outliers, weird shapes
**Examples**:
- x vs y plots
- histograms
- Box Plot ![[Pasted image 20220426103822.png]]
- matrix plot: examples vs feature
	- correlation plot
- scatterplots