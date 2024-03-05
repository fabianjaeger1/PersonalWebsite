---
title: "Machine Learning Overview"
date: 2020-09-15T11:30:03+00:00
# weight: 1
# aliases: ["/first"]
tags: ["first"]
author: "Me"
math: true
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: true
# description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: false
ShowPostNavLinks: true
ShowWordCount: false
ShowRssButtonInSectionTermList: false
UseHugoToc: true
cover:
    image: "" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---


## Regression Problem

**Different Types of Regressions**
_Example used:_ Build a model to predict housing prices. Included metrics are population, median income and median housing price.

- Multiple [Regression](https://en.wikipedia.org/wiki/Regression_analysis): use multiple feature (use district population, the median income) s to make a prediction 
Additionally

- Univariate [[Regression]]: only predict a single value for the output
- Multivariate [[Regression]]: predict multiple values per district

**Performance Measure**
Typical Performance measures for regression problems is the _Root Mean Square Error_


#### Typical Setup with Neural Networks

When building a Multilayer Perceptron for regression, you do not want to use any activation function for the output neurons, so they are free to output any range of values.

| Hyperparameter             | Typical Value                                                                      |
| -------------------------- | ---------------------------------------------------------------------------------- |
| # of input neurons         | One neuron per input feature                                                       |
| # hidden layers            | Depends on the problem, but typically 1 to 5                                       |
| # neurons per hidden layer | Depends on the problem, but typically 10 to 100                                    |
| # output neurons           | 1 per prediction dimension                                                         |
| Hidden activation          | ReLU (or SELU)                                                                     |
| Output activation          | None, or ReLU/softplus (if positive outputs) or logistic/tanh (if bounded outputs) |
| Loss function              | MSE or MAE/Huber (if outliers)                                                     |


## Classification Problem

There are in general three different classification we distinguish between
- Binary Classification Problem
- Multi-class Classification Problem
- Multilabel Classification Task

#### Typical Setup with Neural Networks

| Hyperparameter          | Binary Classification | Multilabel binary Classification | Multiclass classification |
| ----------------------- | --------------------- | -------------------------------- | ------------------------- |
| Input and hidden layers | Same as regression    | Same as regression               | Same as regression        |
| Nr. output neurons      | 1                     | 1 per label                      | 1 per class               |
| Output layer activation | Logistic              | Logistic                         | Softmax                   |
| [[Loss function]]       | Cross entropy         | Cross Entropy                    | Cross Entropy             |

