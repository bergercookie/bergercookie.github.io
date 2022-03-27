---
author: bergercookie
categories:
- scratchpad
- machine-learning
- programming
comments: true
date: "2019-10-14T00:00:00Z"
draft: false
title: Scratchpad - Machine Learning
showtoc: true
---

**Definition:** The science/art of *programming computers* so that they can
learn from data

## Popular ML Algorithms

* Linear & Polynomial Regression
* Logistic Regression
* k-nearest Neighbors
* Support Vector machines
* Decision Trees
* Random Forests
* Ensemble methods

## Neural Networks Architectures

* Feedforward Neural Nets
* Convolutional Nets
* Recurrent Nets
* Long short-term memory (LSTM) nets
* Autoencoders
* Multi-Layer Perceptons (MLPs)

## Famous Papers

* Machine Learning on handwritten digits - 2006 - <www.cs.toronto.edu/~hinton>
* The Unreasonable Effectiveness of Data - 2009


## Useful links - resources

* www.kaggle.com/
  * Competitions
  * Datasets
  * Kernels
* OpenAI Gym
  * For reinforcement learning
* scikit-learn user guide
* Dataquest - www.dataquest.io
* deep learning website - <http://deeplearning.net>
* Imperial College Course
  * <https://www.deeplearningmathematics.com/slides-materials/>
  * <https://github.com/pukkapies/dl-imperial-maths>
* Machine Learning - The Complete Guide <https://en.wikipedia.org/wiki/Book:Machine_Learning_%E2%80%93_The_Complete_Guide>
* <https://paperswithcode.com/>


## Hands-On Machine Learning Book

For the DL part see [Deep Learning]

## Pandas / Sklearn / Numpy / Scipy Cheatsheet

`dt.describe()` → statistics about each column (count, mean, min, max 25% 50% etc.)
`dt.info()` → info about dataframe (dtype index, column dtypes, not-null values, memory usage)
`dt["a_col"].value_counts()` → get all the values encountered in the column
`dt.corr()` → Compute standard correlation coefficient for potential *linear* correlations

{{< highlight python >}}
from pandas.plotting import scatter_matrix
scatter_matrix(dt, figsize=(12,8))
{{< / highlight >}}

Apply a function to a dataframe: either `dt.apply` or `dt.where(... , inplace=True)`

Use the *viridis* color palette: color-blind-friendly and prints better on greyscale!

   <https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html>

### SkLearn - fill missing values in a dataset:

{{< highlight python >}}
from sklearn.preprocessing import Imputer
imputer = Imputer(strategy="median")
imputer.fit(dt) # dt must have numerical values only
{{< / highlight >}}

#### Strategies:

* Get rid of corresponding districts
* Get rid of the whole attribute
* Set the values to some value (zero, mean, median, etc.)

Pandas/SkLearn: Convert a string column/category to nums

{{< highlight bash >}}
dt_encoded, dt_categories = dt.factorize()
# OR Use One-Hot Encoding - each string in the string category becomes a
# separate attribute
sklearn.preprocessing.OneHotEncoder
{{< / highlight >}}

Get Numpy dense array from Scipy sparse matrix: `sparse_mat.toarray()`

#### Feature Scaling

Machine Learning algorithms don't perform well when the input numerical
attributes have very different scales.

* min-max scaling / normalization
* standardization


### Definitions

Attribute: A data type (e.g., Mileage)
Feature: Attribute + its value

#### Deep Neural Network

LTU: Neuron, a Sum using weights -> z = w1x1 + w2x2 + ... + wnxn (w^Tx), gives
out a step function -> e.g., Heaviside

Perceptron -> single Layer of LTUs, Each neuron is connected to all input. The
enuron's are also fed an extra bias feature x0 = 1 (`bias neuron`)

`Passthrough Input Layer`: Inputs are represented by *neurons* that just
propagate the input to the output

Activation function (`activation_fn`): The function that evaluates the neuron
inputs and dicides on the triggering of the neuron

`ReLU or Rectifier or Ramp` -> `max(0, z)`

Hint: The derivative of ReLU is the `Heaviside` and of the SmoothReLU the
`logistic function`


#### Deep Learning Theorems

* [Universal Approximation Theorem](https://en.wikipedia.org/wiki/Universal_approximation_theorem)
* [No Free Lunch Theorem](https://en.wikipedia.org/wiki/No_free_lunch_theorem>)

	Any two optimization algorithms are equivalent when their performance is
	averaged across all possible problems


## FAQ

* How do I tune the hyperparameters of my model?
	* Grid search with cross-validation to find the right hyperparameters
	* Randomised search
	* Use Oscar - <http://oscar.calldesk.ai/>
    * It helps to have an idea of what values are reasonable for each
      hyperparameter!
