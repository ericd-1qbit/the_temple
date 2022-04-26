# Exploratory Data Analysis
https://www.cs.ubc.ca/~schmidtm/Courses/340-F19/L2.pdf
## Typical Cookbook

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
#### Categorical Data
- **frequencies**: number of occurences of different classes
- **mode**: category that occurs most often
- **quantiles** : categories that occur more than t times

#### Continuous Data
- single descriptive metrics:
	- mean: average value
	- median: half-point - 50% of data are smaller/larger
	- quantiles: a fraction k of points
