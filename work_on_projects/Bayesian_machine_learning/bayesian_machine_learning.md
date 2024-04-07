---
title: "Bayesian Machine Learning"
date: 
# weight: 1
# aliases: ["/first"]
tags: ["first"]
author: "Fabian Jaeger"
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


**Abstract:**
*This concise overview introduces Bayesian Neural Networks (BNNs) as a promising alternative to standard neural networks (SNNs), which often suffer from a lack of interpretability, earning them the label of "black box" models. This lack of transparency to a neural network's ability to explain its predictions is especially critical in the sciences and medicine where point estimates are not sufficient and uncertainty estimates are often required. Furthermore, it is argued that incorporating Bayesian concepts into machine learning can also improve the overall accuracy of models. After an introduction and comparison between BNNs and SNNs, in line with the paper from Wilson et. al. \cite{wilson2022a}, we introduce the current understanding of a model's ability to generalize and current shortcomings, such as double descent that plagues standard neural networks, and how certain BNN frameworks prove to be a promising candidate in alleviating some of those pitfalls. However, BNNs still suffer from practical implementations due to their inferior scalability to larger datasets and models. Some of the most common approximations to the optimization of training and estimation of Bayesian statistical quantities are then introduced.*


# Bayesian Neural Networks

Modern deep-learning methods are incredibly powerful tools that can tackle a wide range of challenging problems. However, due to their nature as black boxes, quantifying the uncertainty associated with their predictions can be difficult [@bykov2021]. Bayesian statistics provide a formal framework to comprehend and measure the uncertainty inherent in deep neural network predictions.

Bayesian Neural Networks incorporate the principles of Bayesian Inference, which can be particularly useful when dealing with limited data or when making predictions in uncertain environments. BNNs extend traditional neural networks by introducing probabilistic weights and biases.

BNNs train the model weights as probability distributions rather than searching for a singular optimal value as with SNN. This makes them more robust and allows them to generalize better with less overfitting. The process of finding these distributions associated with the weights is called *marginalization*.

One standard approach to finding point estimates of weights in standard neural networks would be Maximum Likelihood Estimators (MLE) while for BNN, the estimate would be rather Maximum A Posteriori (MAP) or predictive distribution. While SNNs would use differentiation to find the optimal value through gradient descent, BNNs rely on Markov Chain Monte Carlo (MCMC), Variational Inference, and Normalizing Flows [@winter2023], given the presence of hard-to-compute integrals which has the unfortunate consequence of increased computational complexity.

## Advantages of BNNs

### Sources of uncertainty

Usually, in SNN applications, our data $\mathcal{D}$ is merely a sample of the process we are modeling. In these cases, we are looking for models that generalize to unseen data. Therefore, it is useful to express the uncertainty about our model due to the lack of data. This uncertainty is commonly referred to as epistemic uncertainty or parameter uncertainty.

BNNs address epistemic uncertainty, as explained above, by treating the model's weights as probabilistic variables rather than fixed parameters. This allows the model to capture the uncertainty in its own parameters and produce probabilistic predictions, indicating the model's confidence in its predictions.

Usually, there is another source of uncertainty called aleatoric uncertainty, which originates directly from the process that we are modeling. This uncertainty, also known as data uncertainty, arises from the inherent variability in the data itself and is the noise in the labels that cannot be explained by the inputs. Often, this uncertainty is called “irreducible noise”. Bayesian Neural Networks play a crucial role in quantifying and managing also aleatoric uncertainty by incorporating uncertainty estimates in the output of the model.

### Bayesian Inference

In Bayesian Inference, given for example some known input-output pairs in a supervised learning setting, we seek to compute the posterior $p(\boldsymbol{\theta}|\mathcal{D})$, which is the conditional distribution of the parameters of a model given the training data $\mathcal{D}$. The posterior can be determined using Bayes' theorem:


$$
p(\boldsymbol{\theta} | \mathcal{D}) = \frac{p(\boldsymbol{\theta}) p(\mathcal{D} | \boldsymbol{\theta})}{p(\mathcal{D})} \propto p(\boldsymbol{\theta}) p(\mathcal{D}|\boldsymbol{\theta})
$$

where $p(\mathcal{D}|\boldsymbol{\theta})$ represents the likelihood and $p(\boldsymbol{\theta})$ the prior.
Our interest in the posterior $p(\boldsymbol{\theta}|\mathcal{D})$ lies in the fact that we want to compute the *posterior predictive distribution* to model unseen data

$$
p(\boldsymbol{y}|\boldsymbol{x},\mathcal{D}) = \int p(\boldsymbol{y}|\boldsymbol{x}, \boldsymbol{\theta} ) p(\boldsymbol{\theta}|\mathcal{D})d\boldsymbol{\theta}= \mathbb{E}_{p(\boldsymbol{\theta}|\mathcal{D})}\left[ p(\boldsymbol{y}|\boldsymbol{x},\mathcal{D}) \right].
$$

Equation \ref{eq:predictive_distribution} represents a *Bayesian Model Average* (BMA) as it averages the predictions of all plausible models weighted by their posterior. This yields a nice interpretation of the predictive distribution as an infinite ensemble of networks, hence *ensemble learning*, which can represent many hypothesis models we believe to be possible. This is in net contrast to MLE methods in SNN where only one set of parameters $\boldsymbol{\theta}^*$, therefore one hypothesized model, is used for predictions.

\begin{center}
\begin{tabular}{ccc}
SNN & & BNN\\
$\boldsymbol{\theta}^*$ & $\Rightarrow$ & $p(\boldsymbol{\theta}|\mathcal{D})$ \\
$y_{\boldsymbol{\theta}^*}(x)$ & $\Rightarrow$ &  $p(\boldsymbol{y}_{\boldsymbol{\theta}}|\boldsymbol{x},\mathcal{D})$ \\
\end{tabular}
\end{center}

An immediate benefit of specifying distributions over the model parameters and predictions is that we can quantify our uncertainty about these things, e.g., by computing their variance. This is especially relevant when learning from small datasets; standard neural net training will overfit for the reasons discussed above, but Bayesian Inference will find the best explanation for the model parameters given the available data, which typically have high uncertainty when data is scarce. In the limit of dataset size far exceeding the number of neurons, the inferred distributions sharpen and begin to resemble the solutions from the standard training; for modern networks we don’t typically reach this limit in practice, so having a notion of model uncertainty is helpful.

The classical training of an SNN can be viewed as a limit of the Bayesian Inference in the case when $p(\boldsymbol{\theta}|\mathcal{D})\approx \delta(\boldsymbol{\theta}=\boldsymbol{\theta}^*)$, where the delta function is zero everywhere except at $\boldsymbol{\theta}^*=\text{argmax}_{\boldsymbol{\theta}}p(\boldsymbol{\theta}|\mathcal{D})$. The difference between a classical and Bayesian approach will depend on how sharp the posterior becomes. If the posterior is sharply peaked and the predictive distribution does not vary much where the posterior has mass, then there may be no difference between the two approac
