---
title:  "MML Introduction"
excerpt: "Introduction of MML"

categories:
  - MML
tags:
  - [MML, Stats]

toc: true
toc_sticky: true
mathjax: true
 
date: 2022-12-21
last_modified_at: 2022-12-22
---
# Mathematics for Machine Learning

(Chapter 1 is Introduction.)

## Part 1 (Mathematics)

### Chapter 2 : Linear algebra

We represent numerical data as vectors and represent a table of such data as a matrix.

The study of vectors and matrices is called linear algebra, which we introduce in Chapter 2.

The collection of vectors as a matrix is also described there.

### Chapter 3 : Analytic geometry

Given two vectors representing two objects in the real world, we want to make statements about their similarity.

The idea is that vectors that are similar should be predicted to have similar outputs by our machine learning algorithm (our predictor).

To formalize the idea of similarity between vectors, we need to introduce operations that take two vectors as input and return a numerical value representing their similarity.

The construction of similarity and distances is central to analytic geometry and is discussed in Chapter 3.

### Chapter 4 : Matrix decomposition

In Chapter 4, we introduce some fundamental concepts about matrices and matrix decomposition.

Some operations on matrices are extremely decomposition useful in machine learning, and they allow for an intuitive interpretation of the data and more efficient learning.

### Chapter 5 : Vector calculus

To train machine learning models, we typically find parameters that maximize some performance measure.

Many optimization techniques require the concept of a gradient, which tells us the direction in which to search for a solution.

Chapter 5 is about vector calculus and details the vector calculus concept of gradients.

### Chapter 6 : Probability theory

We often consider data to be noisy observations of some true underlying signal.

We hope that by applying machine learning we can identify the signal from the noise.

This requires us to have a language for quantifying what “noise” means.

We often would also like to have predictors that allow us to express some sort of uncertainty, e.g., to quantify the confidence we have about the value of the prediction at a particular test data point.

Quantification of uncertainty is the realm of probability theory and probability theory is covered in Chapter 6.

### Chapter 7 : Optimization

Chapter 7 is optimization to find maxima/minima of functions.

## Part 2 (Machine Learning)

### Chapter 8 : Set-up

In Chapter 8, we restate the three components of machine learning (data, models, and parameter estimation) in a mathematical fashion.

In addition, we provide some guidelines for building experimental set-ups that guard against overly optimistic evaluations of machine learning systems.

Recall that the goal is to build a predictor that performs well on unseen data.

### Chapter 9 : Linear regression

In Chapter 9, we will have a close look at linear regression, where our objective is to find functions that map inputs \\( x \in \mathbb {R}^D\\) to corresponding observed function values \\( y \in \mathbb {R}\\), which we can interpret as the labels of their respective inputs.

We will discuss classical model fitting (parameter estimation) via maximum likelihood and maximum a posteriori estimation, as well as Bayesian linear regression, where we integrate the parameters out instead of optimizing them.

### Chapter 10 : Dimensionality reduction

Chapter 10 focuses on dimensionality reduction using principal component analysis.

The key objective of dimensionality reduction is to find a compact, lower-dimensional representation of high-dimensional data \\( x \in \mathbb {R}^D\\), which is often easier to analyze than the original data.

Unlike regression, dimensionality reduction is only concerned about modeling the data – there are no labels associated with a data point \\(x\\).

### Chapter 11 : Density estimation

In Chapter 11, we will move to our third pillar: density estimation.

The objective of density estimation is to find a probability distribution that describes a given dataset. We will focus on Gaussian mixture models for this purpose, and we will discuss an iterative scheme to find the parameters of this model.

As in dimensionality reduction, there are no labels associated with the data points \\( x \in \mathbb {R}^D\\).

However, we do not seek a low-dimensional representation of the data.

Instead, we are interested in a density model that describes the data.

### Chapter 12 : Classification

Chapter 12 concludes the book with an in-depth discussion of classification.

We will discuss classification in the context of support vector machines.

Similar to regression (Chapter 9), we have inputs x and corresponding labels y.

However, unlike regression, where the labels were real-valued, the labels in classification are integers, which requires special care.

## Exercises and programming tutorials

[https://mml-book.com](https://mml-book.com)
