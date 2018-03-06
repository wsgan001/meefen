---
layout: post
categories: notes
title: 'Notes:  neuralnet: Training of neural network'
tags:
- machine learning
- analytics
---

## References

**Citekey**: @gunther2010neuralnet

Gu ̈nther, F. and Fritsch, S. (2010). neuralnet: Training of neural networks. The R journal, 2(1):30–38.


## Notes

This article introduces `neuralnet` -- an R package that trains supervised neural networks.

## Highlights


There are two other packages that deal with artificial neural networks at the moment: nnet (Venables and Ripley, 2002) and AMORE (Limas et al., 2007). nnet provides the opportunity to train feed-forward neural networks with traditional backpropagation and in AMORE, the TAO robust neural network algorithm is implemented. (p. 1)

neuralnet was built to train neural networks in the context of regression analyses. Thus, resilient backpropagation is used since this algorithm is still one of the fastest algorithms for this purpose (p. 1)

Artificial neural networks can be applied to approximate any complex functional relationship. Unlike generalized linear models (GLM, McCullagh and Nelder, 1983), it is not necessary to prespecify the type of relationship between covariates and response variables as for instance as linear combination. (p. 1)

Multi-layer perceptrons (p. 1)

The package neuralnet focuses on multi-layer perceptrons (MLP, Bishop, 1995), which are well applicable when modeling functional relationships. (p. 1)

The package neuralnet (Fritsch and Günther, 2008) contains a very flexible function to train feedforward neural networks (p. 1)

Supervised learning (p. 2)

Neural networks are fitted to the data by learning algorithms during a training process. neuralnet focuses on supervised learning algorithms. (p. 2)

During an iterative training process, the following steps are repeated: (p. 2)

To increase the modeling flexibility, hidden layers can be included. However, Hornik et al. (1989) showed that one hidden layer is sufficient to model any piecewise continuous function. (p. 2)

A widely used learning algorithm is the resilient backpropagation algorithm. (p. 3)

The resilient backpropagation algorithm is based on the traditional backpropagation algorithm that modifies the weights of a neural network in order to find a local minimum of the error function. (p. 3)

In order to speed up convergence in shallow areas, the learning rate ηk will be increased if the corresponding partial derivative keeps its sign. On the contrary, it will be decreased if the partial derivative of the error function changes its sign since a changing sign indicates that the minimum is missed due to a too large learning rate. (p. 3)

Unlike the traditional backpropagation algorithm, a separate learning rate ηk, which can be changed during the training process, is used for each weight in resilient backpropagation. (p. 3)

Using neuralnet (p. 4)

Its usage is leaned towards that of functions dealing with regression analyses like lm and glm. As essential arguments, a formula in terms of response variables ̃ sum of covariates and a data set containing covariates and response variables have to be specified. (p. 4)

The function neuralnet used for training a neural network provides the opportunity to define the required number of hidden layers and hidden neurons according to the needed complexity. (p. 4)

Visualizing the results (p. 6)

The results of the training process can be visualized by two different plots. First, the trained neural network can simply be plotted by > plot(nn) (p. 6)

The second possibility to visualize the results is to plot generalized weights. gwplot uses the calculated generalized weights provided by nn$generalized.weights and can be used by the following statements: > par(mfrow=c(2,2)) > gwplot(nn,selected.covariate="age", + min=-2.5, max=5) (p. 6)
