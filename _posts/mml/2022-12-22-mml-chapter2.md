---
title:  "Chapter 2 : Linear Algebra (작성중)"
excerpt: "Linear Algebra"

categories:
  - MML
tags:
  - [MML, Stats]

toc: true
toc_sticky: true
mathjax: true
 
date: 2022-12-22
last_modified_at: 2022-12-22
---
## Vectors

> **Vectors** are special objects that can be added together and multiplied by scalars to produce another object of the same kind.

Some examples of vector objects.

1. Geomatric vectors.
2. Polynomials.
3. Audio signals.
4. **Elements of \\( \mathbb {R}^n \\) (tuples of \\( n \\) real numbers)** \\( \Leftarrow \\) This is the concept we should focus 👀️

## Closure

> **Closure** : What is the set of all things that can result from my proposed operations?

What is the set of vectors that can result by adding and scaling? (=**Vector space**)


## Matrix

### Coefficient to Vector, Vector to Matrix

$$
a_{11}x_{1} + \dots + a_{1n}x_{n} = b_1
\newline\vdots\newline
a_{m1}x_{m} + \dots + a_{mn}x_{n} = b_m

$$

into

$$
\begin{bmatrix}
a_{11} \\ 
\vdots \\ 
a_{m1}
\end{bmatrix}
x_1
+
\begin{bmatrix}
a_{12} \\ 
\vdots \\ 
a_{m2}
\end{bmatrix}
x_2+
\dots+
\begin{bmatrix}
a_{1n} \\ 
\vdots \\ 
a_{mn}
\end{bmatrix}
x_n =
\begin{bmatrix}
b_{1} \\ 
\vdots \\ 
b_{m}
\end{bmatrix}

$$

$$
\begin{bmatrix}
a_{11} & \dots & a_{1n} \\ 
\vdots & \ddots & \vdots \\ 
a_{m1} & \dots & a_{mn}
\end{bmatrix}

\begin{bmatrix}
x_{1} \\ 
\vdots \\ 
x_{n}
\end{bmatrix}

=

\begin{bmatrix}
b_{1} \\ 
\vdots \\ 
b_{n}
\end{bmatrix}

$$

$$
A=\begin{pmatrix}
a_{11} & a_{12} & \dots & a_{1n} \\ 
a_{21} & a_{22} & \dots & a_{2n} \\ 
\vdots & \vdots & \ddots & \vdots \\ 
a_{m1} & a_{m2} & \dots & a_{mn}
\end{pmatrix}

$$
