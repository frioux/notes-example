---
title: Machine learning
date: 2017-12-23T08:30:40
tags: [ public, project ]
guid: 0a1b7f49-a33e-405d-b93e-3c29be218fc5
---


<!--more-->

## Next Steps

 * [Take other classes](http://deeplearning.ai)
 * Read Deep Learning Book

**Note:** These notes were started in the middle of the class, so they are
likely not of much use to others.

## Evaluating a Hypothesis

Instead of using all data for training, split data into three parts:

 1. ~60% for training.
 2. ~20% for validation.
 3. ~20% for testing.

Use the training data to train your hypotheses, then use validation to select
the winning hypothesis, then use testing the validate that the hypothesis.

If the cost of the training and the validation are both high (and basically
equal,) you have *high bias* (*underfit*.)

If the cost of the training is low but the cost of the validation is
significantly higher you have *high variance* (*overfit*.)

This can be seen if you plot the cost of the training data and the cost of the
validation data against the degree of polynomial.

## Regularization and Bias / Variance

Define the cost function to include the regularization parameter; leave it off
for the cost for training, validation, and testing.

For various lambdas (0, 0.01, 0.02, 0.04, 0.08 .. 10~) minimize the cost
function with the training cost function.  Select the minimized theta that has
the lowest error on the unregularized cost function against the validation set.

Finally, apply the test cost function to see how well theta generalizes.

## Learning Curves

Pick a subset of your training data starting at m=1 and going to the size of the
training data.  As m increases you will find that you can no longer fit each
data point perfectly and that error will increase.

On the other hand, when starting with m=1 with the *cross validation* set, the
lower the amount of data used the *higher* the error will be.

### High Bias (aka underfit)

When plotting a learning curve in a high bias situation, you will find that
fairly quickly your curve flattens out, since your curve is just poorly fit in
general.  Unlike in a more optimal situation, when the bias is high, the
training and cross validation errors will end up being very close or the same.

Relatively high error.

> If a learning algorithm is suffering from high bias, getting more training
> data won't really help.

### High Variance (aka overfit)

When plotting a learning curve in a high variance situation, you will find that
error is zero for training data, but high for cross validation data.

Large gap between training error and cross validation error.

> If a learning algorithm is suffering from high variance, getting more training
> data is likely to help.

## Debugging a Learning Algorithm

You have implemented a learning algorithm but it is found wanting.  Here are
some options and why you might use then:

 * Have high variance?
   * Get more training data
   * Try fewer features
   * Try increasing λ
 * Have high bias?
   * Get additional features
   * Try adding polynomial features
   * Try increasing λ

 * Small neural networks (few hidden layers, few nodes)
   * More prone to high bias
   * Computationally cheaper
 * Large neural networks (many hidden layers, many nodes)
   * More prone to high variance
   * Computationally expensive
   * Use regularization to handle overfit
   * For picking hidden layer count, use the normal train / cross validation
     checking

## Getting Started on a Machine Learning implementation

 1. Implement the most basic version that could work, in 24 hours our less, to
    build out the tooling to test a cross validation set.

 2. Plot learning curves to decide if more data, more features, will help.

 3. Use Error Analysis to example the individual data points that the algorithm
    had high error and see if there are any systematic errors.

Critically, you need a way to get a number (3% error, for example) so that you
can easily compare different varieties of your algorithm (like with or without
stemming, case sensitive or case insensitive, etc.)

## Error Analysis for Skewed Classes

You might think that you are a golden god because you have implemented an
algorithm that gets the right answer for a gigantic data set of medical data,
classifying cancer.  Concretely it might be right 99% of the time.  The bad news
is that because the occurance of cancer in the data set is so low (%0.5) it's
actually *worse* than assuming literally no one has cancer.  Woops.

Guess: scale error by ratio?  Maybe have error per class?

### Precision/Recall

|                        |  Cancerous | Noncancerous |
|----------------------- |------------|--------------|
| Predicted Cancerous    | true pos   | false pos    |
| Predicted Noncancerous | false neg  | true neg     |

**Precision**: Of all the patients where we guessed they have cancer, what fraction
actually do? For example if when we decided "cancer" and were always correct,
but missed half of the cancer patients, we'd have a 100% precision.

```
precision =
  true positives / predicted positives =
  true positives / (true positives + false positives)
```

**Recall**: Of all of the cancer patients, what fraction did we decide correctly?
In the example above we'd have a 50% recall.

```
recall =
  true positives / actual positives =
  true positives / (true positives + false negatives)
```

Note that this is specifically set such that the rare class is the true case.

## How to control the Precision/Recall Tradeoff

You can increase precision by increasing the requirement for y to be true.  So
normally you say y is true if the hypothesis is over 0.5; instead you might
increaes the requirement so that the hypothesis has to be over 0.7.  This will
increase precision, but decrease recall.

## F score to compare Precision/Recall values

```
2 * P * R / (P + R)
```

## Does having "lots" of data help?

 1. Assume that we have enough feature data (ie if a human expert looked at the
 sample, they would be able confidently make a correct decision)

 2. Use a "low bias" algorithm via many parameters; like a neural network with
    many hidden layers or logistic/linear regression with many features.

 3. A large dataset is very unlikely to overfit.

## Support Vector Machines

Basically, instead of the complicated function that logistic regression is based
on, SVM uses three or four basic line segments, thus making it *much* easier to
compute.

Logistic Regression Cost Function:
![cost function](../../img/machine-learning-lin-reg.png)

SVM Cost Function:
![cost function](../../img/machine-learning-svm.png)

SVM Hypothesis:
![cost function](../../img/machine-learning-svm-hyp.png)

As a side effect of the cost function, SVM have large margins, picking
boundaries that increase the "space" between samples.

## Kernels

Given x, compute new features depending on proximity to landmarks.

There are various kernels, the one defined in class is called the Gaussian
kernel.  They are all "similarity functions."

Each landmark maps to a feature.

## Landmarks

Place a landmark at each training data location.

## SVM Parameters

```
C = 1 / λ
```

 * C
    * Large C: Lower bias / High variance
    * Small C: Lower variance / High bias
 * Choice of kernel (similarity function)
    * No kernel (linear); for when n is large, m is small
    * Gaussian kernel; for when n is small, and/or m is large
       * Choose σ²
          * Large σ²: Features vary more smoothly, Higher bias, lower variance.
          * Small σ²: Features vary more abruptly, Higher variance, lower bias.
       * Must performe feature scaling *before* using Gaussian kernel.
    * You may need to implement the kernel function yourself.

Not all similarity functions are kernels.

Other kernels (much more rare:)

 * Polynomial
 * String
 * chi-squared
 * histogram
 * intersection

## Multi-class Classification

Typically built in, otherwise implement one-vs-all classification.

## Logistic Regression vs SVM

When there are many features (n) compared to the amount of samples (m), use
logistic regression or SVM without a kernel.  Like if n >= m, n = 10k, m =
10..1k.

When there are few features (1..1000) and an intermediate number of samples
(10..10,000), use SVM with Gaussian kernel.

When there are few features (1..1000) and many samples (50,000+) create or add
more features, then use logistic regression or SVM without a kernel, otherwise
it will be too slow.

Neural network works well for all of the above, but is slower to train.

## Principle Component Analysis

Always perform mean normalization, and probably perform feature scaling.

```
sigma = (1/m) * X' * X;
[U,S,V] = svd(sigma);
Ureduce = U(:,1:k);
z = Ureduce'*x;
```

 * PCA can be used to speed up Machine Learning
 * PCA *cannot* be used to avoid overfitting

## Anomaly Detection Algorithm

 1. Choose feature `x_i` that you think might be indicative of anomalous examples.
 2. Fit parameters μ₁,...,μₙ,σ₁²,...,σₙ²

```
u_j = 1/m * sum of the examples of feature j
sigma_j = 1/m * sum of (x_j - u_j)^2
```

 3. Given new example x, compute `p(x)`

## Algorithm Evaluation

Possible evaluation metrics:

 * True positive, false positive, true negative, false negative
 * Precision/Recall
 * F-1 Score

Use CV to choose ε.

## Anomaly Detection vs Supervised Learning

Anomaly Detection:

 * Very small number of positive examples (0-20)
 * Large number of negative examples.
 * Many different "types" of anomalies.
 * Future anomalies may look nothing like any of the examples we've seen so far.
 * Examples
   * Fraud Detection
   * Manufacturing
   * Monitoring machines in a data center

Supervised Learning

 * Large number of positive and negative examples.
 * Examples
   * Spam Classification
   * Weather prediction
   * Cancer Classification

## Non-gaussian features

 * Maybe use a transformation (like `log(x)`, `log(x+1)`, `sqrt(x)`) to make it
   normal
 * Plot histogram, play around

## Error Analysis for Anomaly Detection

Want `p(x)` large for normal examples, small for anomalous examples.

Most common problem:

`p(x)` is comparable for normal and anomalous examples.

## Monitoring computers in a data center

Choose features that might take on unusually large or small values in the event
of an anomaly:

 * memory use
 * number of disc accesses/sec
 * cpu load
 * network traffic
 * if cpu load and network traffic are linked, maybe do
   cpu load / network traffic

## Multivariate Gaussian distribution

Don't model probabilities separately, model p(x) all in one go.

## Original vs Multivariate

Multivariate automatically captures correlations between features.  m must be >
n, or else the sum is non invertable.

For original you have to manually create features to capture anomalies where x
and y take unusual combinations of values (like `x3 = x1/x2`.)  Original is
computationally cheaper. (works with n=10,000 or n=100,000, and when m is small)

## Recommendation Systems

`r(i,j) = 1` if user j has rated movie i

`y(i,j) = rating` by user j on movie i

`θ(j) = parameter vector for user j`

`x(i) = feature vector for movie i`

For user j, movie i, predicted rating: `(θ(j)'(x(i)))`

`m(j) = no of movies rated by user j`

## Recommendation Systems Optimization Objective

![objective](../../img/machine-learning-rec-sys-opt-obj.png)

## Recommendation Systems Gradient Descent

![gradient descent](../../img/machine-learning-rec-sys-grad-desc.png)

## Recommendation Systems Colaborative Filtering

Treat features as unknowns, but ask users for their personal feature ratings
(aka θ(j).

## Recommendation Systems Optimization Algorithm

![optimization algorithm](../../img/machine-learning-rec-sys-opt-alg.png)

![optimization algorithm 2](../../img/machine-learning-rec-sys-opt-alg-2.png)

Now estimate movie preferences, then improve human preferences, recursively.

## Collaborative filtering algorithm

 1. Initialize x(1),...,x(n_m),θ(1),...,θ(n_u) to small random values.
 2. Minimize J(x(1),...,x(n_m),θ(1),...,θ(n_u)) using gradient descent (or
    something else); Eg. for ![collaborative filtering algorithm](../../img/machine-learning-col-filt-alg.png)
 3. For a user with parameters θ and a movie with (learned) features x, predict
    a star rating of θ'x

## Colaborative Filtering aka Low Rank Matrix Factorization

![low rank](../../img/machine-learning-low-rank.png)

## To find related movies

A small `||x(i) - x(j)||` implies similar movies

## For users who have not rated any movies

Use mean normalization so that a "zero" users likes movies based on the average
rating.

## Large Scale Machine Learning

 * Use [Learning Curves](#learning-curves), plotting against m, to discover if
   adding data will help.

## Stochastic Gradient Descent

 * Shuffle data set
 * Take steps based on each example, instead of all examples.
 * calculate cost **before updating θ**
   * Every 1000 interations, "plot" average cost, to inform user of convergence
 * To force convergence, decrease α each iteration

## Mini-Batch Gradient Descent

 * Pick mini-batch size b (2-100 is typical.)
 * Perform gradient descent update using b examples.
 * This will outperform Stochastic GD if you have good vectorization.

## Online Learning

 * Learn from one example at a time, and throw it away without retraining
 * Can adapt to changing user preference
 * Might use this to build a search engine, sorting by predicted CTR

## Map Reduce

 * Basically do batch gradient descent, but divide up summing per machine

## Links

 * [AI::FANN - Perl wrapper for the Fast Artificial Neural Network library - metacpan.org](https://metacpan.org/pod/AI::FANN)
 * [Fast Artificial Neural Network Library (FANN)](http://leenissen.dk/fann/wp/)
 * [A Neural Network Playground](http://playground.tensorflow.org/)
 * [RL Course by David Silver - Lecture 1: Introduction to Reinforcement Learning - YouTube](https://www.youtube.com/watch?v=2pWv7GOvuf0&list=PL5X3mDkKaJrL42i_jhE4N-p6E2Ol62Ofa)
 * [Sutton & Barto Book: Reinforcement Learning: An Introduction](http://webdocs.cs.ualberta.ca/~sutton/book/the-book.html)
 * [Deep Learning](http://www.deeplearningbook.org/)
 * [Deep Learning Classes](https://www.deeplearning.ai/)
 * [NIPS 2017 Notes](https://cs.brown.edu/~dabel/blog/posts/misc/nips_2017.pdf)
 * [Computer Vision Lessons Learned](https://www.kdnuggets.com/2017/12/ng-computer-vision-11-lessons-learnied.html)
