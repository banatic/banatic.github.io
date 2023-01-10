---
title:  "Chapter 2-1 : 행렬의 기본적 성질"
excerpt: "Linear Algebra"

categories:
  - 선형대수학
tags:
  - [벡터]

toc: true
toc_sticky: true
mathjax: true
 
date: 2022-12-22
last_modified_at: 2023-01-05
---
## Vectors

> **Vectors** are special objects that can be added together and multiplied by scalars to produce another object of the same kind.

Some examples of vector objects.

1. Geomatric vectors.
2. Polynomials.
3. Audio signals.
4. **Elements of $ \mathbb {R}^n $ (tuples of $n$ real numbers)** $ \Leftarrow $ This is the concept we should focus 👀️

$$
\begin{bmatrix}
1 \\
2 \\
3 \\
\end{bmatrix}
$$

## Closure

> **Closure** : What is the set of all things that can result from my proposed operations?

What is the set of vectors that can result by adding and scaling? (=**Vector space**)


## Matrix

### Definition

With $ m, n \in \mathbb{N}^n $, a real-valued $(m, n)$ matrix $A$ is an $ m\cdot n$-tuple of elements $a_{ij},\; i=1, \dots ,m, \; j=1, \dots, n,$ which is ordered according to a rectangular scheme consisting of $m$ rows and $n$ columns:

$$
A =
\begin{bmatrix}
a_{11} & \dots & a_{1n} \\ 
\vdots & \ddots & \vdots \\ 
a_{m1} & \dots & a_{mn}
\end{bmatrix}, \quad a_{ij} \in \mathbb R
$$

$ \mathbb R^{m \times n} $ is the set of all real-valued $(m, n)$-matrices.

$ A \in \mathbb{R}^{m \times n}$ can be equivalently represented as $a \in \mathbb R^{mn}$ by stacking all $n$ columns of the matrix into a long vector.

### Coefficient to Vector, Vector to Matrix
1. Polynomial Coefficient

$$
a_{11}x_{1} + \dots + a_{1n}x_{n} = b_1 \\ 
\vdots \\
a_{m1}x_{m} + \dots + a_{mn}x_{n} = b_m
$$

2. Into Vector

$$
\begin{bmatrix}
a_{11} \\ \vdots \\ a_{m1}
\end{bmatrix}
x_1+
\begin{bmatrix}
a_{12} \\ \vdots \\ a_{m2}
\end{bmatrix}
x_2+
\dots+
\begin{bmatrix}
a_{1n} \\ \vdots \\ a_{mn}
\end{bmatrix}
x_n =
\begin{bmatrix}
b_{1} \\ \vdots \\ b_{m}
\end{bmatrix}
$$

3. Into Matrix

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
\end{bmatrix}=
\begin{bmatrix}
b_{1} \\ 
\vdots \\ 
b_{n}
\end{bmatrix}
\\
$$

- - -

### Operation

#### Addition
The sum of two matrices $A \in \mathbb R^{m \times n}, B \in \mathbb R^{m \times n}$ is defined as the element-wise sum.

$$
A + B :=
\begin{bmatrix}
a_{11} + b_{11} & \dots & a_{1n} + b_{1n} \\ 
\vdots & \ddots & \vdots \\ 
a_{m1} + b_{m1} & \dots & a_{mn} + b_{mn}
\end{bmatrix}
\in \mathbb R^{m \times n}.
$$

#### Multiplication
For matrices $A \in \mathbb R^{m \times n}, B \in \mathbb R^{n \times k}$, the elements $c_{ij}$ of the product $ C=AB \in \mathbb R^{m \times k} $ are computed as

$$
c_{ij} = \sum_{l=1}^{n}a_{il}b_{lj}, \quad i=1, \;\dots\; ,m, \quad j=1,\;\dots\;,k.
$$

We call this ***dot product***. Matrices can only be multiplied if their "neighboring" dimensions match. And remark that dot product isn't defined as element-wise.

Element-wise multiplication is called ***Hadamard product***.

##### Identity Matrix

In $ \mathbb R^{n \times n}$, we define the **identity matrix** as the $ n \times n$-matrix containing 1 on the diagonal and 0 everywhere else.

$$
I_n :=
\begin{bmatrix}
1 & 0  & \dots & 0 & \dots & 0 \\ 
0 & 1  & \dots & 0 & \dots & 0 \\ 
\vdots & \vdots & \ddots & \vdots & \ddots& \vdots \\
0 & 0  & \dots & 1 & \dots & 0 \\ 
\vdots & \vdots & \ddots & \vdots & \ddots& \vdots \\
0 & 0  & \dots & 0 & \dots & 1 \\ 
\end{bmatrix}
\in \mathbb R^{n \times n}
$$

#### Inverse

Consider a square matrix $A \in \mathbb R^{n \times n}$. Let matrix $ B \in \mathbb R^{n \times n}$ have the property that $AB = I_n = BA$. 
$B$ is called the *inverse* of $A$ and denoted by $A^{-1}$

Not every matrix possesses an inverse. If this inverse does exist, matrix is called *regular/invertible/nonsingular*, otherwise *singular/noninvertible*.

Consider a matrix

$$
A := \begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{bmatrix} \in \mathbb R^{2 \times 2}.
$$

If we multiply $A$ with

$$
A' := \begin{bmatrix} a_{22} & -a_{12} \\ -a_{21} & a_{11} \end{bmatrix}
$$

we obtain

$$
AA' = \begin{bmatrix} a_{11}a_{22} - a_{12}a_{21} & 0 \\ 0 & a_{11}a_{22} - a_{12}a_{21} \end{bmatrix} = (a_{11}a_{22}-a_{12}a_{21})I.
$$

Therefore,

$$
A^{-1} = \frac{1}{a_{11}a_{22}-a_{12}a_{21}} \begin{bmatrix} a_{22} & -a_{12} \\ -a_{21} & a_{11} \end{bmatrix}
$$

**if and only if $\boldsymbol{a_{11}a_{22}-a_{12}a_{21} \neq 0}$.**

We call $a_{11}a_{22}-a_{12}a_{21}$ *determinant* of a $2 \times 2$-matrix and generally use to check whether a matrix is invertible.

#### Transpose

For $A \in \mathbb R^{m \times n}$ the matrix $B \in \mathbb R^{n \times m}$ with $b_{ij} = a_{ji}$ is called the *transpose* of $A$ and write $B=A^T$


#### Symmetric
A matrix $A \in \mathbb R^{n \times n}$ is *symmetric* if $A=A^T$.
The sum of symmetric matrices is always symmetric.

#### Multiplication by a Scalar

Let us look at what happens to matrices when they are multiplied by a scalar $ \lambda \in \mathbb R$. 
Let $A \in \mathbb R^{m \times n}$ and $\lambda \in \mathbb R$. Then $\lambda A = K, K_{ij} = \lambda a_{ij}$.
Practically, $\lambda$ scales each element of $A$.

- - - 

### Properties

**Associativity**

$$ 
\forall A \in \mathbb R^{m \times n}, B \in \mathbb R^{n \times p},C \in \mathbb R^{p \times q} : (AB)C = A(BC) 
$$

$$ 
(\lambda \psi)C = \lambda(\psi C), C \in \mathbb R^{m \times n}\\
\lambda(BC) = (\lambda B)C = B(\lambda C) = (BC)\lambda, \quad B \in \mathbb R^{m \times n}, \; C \in \mathbb R^{n \times k}
$$

**Distributivity**

$$ \begin{split} \forall A , B \in \mathbb R^{m \times n},\; C, D \in \mathbb R^{n \times p} : (A+B)C = AC + BC \\ A(C+D) = AC + AD \end{split} $$

$$ 
(\lambda \psi)C = \lambda C + \psi C, \quad C \in \mathbb R^{m \times n}\\
\lambda(B+C) = \lambda B + \lambda C, \quad B, C \in \mathbb R^{m \times n} 
$$


**Multiplication with the identity matrix**

$$ \forall A, B \in \mathbb R^{m \times n} : I_mA=AI_n=A $$

**Inverses and transposes**

$$
(\lambda C)^T = C^T\lambda ^T = C^T\lambda = \lambda C^T\\
\text{since}\; \lambda=\lambda^T \; \text{for all}\; \lambda \in \mathbb R
$$

$$
\begin{split}
AA^{-1} &= I = A^{-1}A\\
(AB)^{-1}&=B^{-1}A^{-1}\\
(A+B)^{-1} &\neq A^{-1}+B^{-1}\\
(A^T)^T &= A\\
(A+B)^T&=A^T+B^T\\
(AB)^T &= B^TA^T
\end{split}
$$

- - -
### np.einsum 함수

** https://ajcr.net/Basic-guide-to-einsum/ 에서 발췌

28p 좌측에 **einsum** 함수를 사용한 짧막한 코드가 적혀있다.
``` Python
C = np.einsum('il,lj', A, B)
```
배열(행렬)에 관한 대다수의 연산을 Einstein summation 컨벤션을 통해 표현할 수 있다. (곱이든, 합이든, 전치든 ... 물론 더 복잡한 연산도 한번에 표현/계산할 수 있다.)
이 Einstein summation 컨벤션을 계산하는 함수가 바로 **einsum**이다.
<span style="color:gray">Einstein notation은 Ricci calculus의 subset이라고 한다.</span>

여러 번의 행렬 연산을 거쳐야 하는 경우, numpy의 다양한 함수를 조합하는 것보다 einsum 함수를 활용하여 한번에 계산하는 것이 속도나 메모리 측면에서 유리하다. 

예시 상황으로 생각해보자.

>Example.
>1. $A$와 $B$를 적절히 전치하여 곱하고,
>2. 그 결과를 한 축을 기준으로 더한다.

einsum 함수의 유무를 비교해보자.

``` Python
>>> A = np.array([0, 1, 2])
>>> B = np.array([[ 0,  1,  2,  3],
                  [ 4,  5,  6,  7],
                  [ 8,  9, 10, 11]])

>>> (A[:, np.newaxis] * B).sum(axis=1)
array([ 0, 22, 76])
# A.T*B를 못하는 이유는, A가 원래 1D이기 때문에 전치를 해도 동일하기 때문이다. 
>>> np.einsum('i,ij->i', A, B)
array([ 0, 22, 76])
```
einsum 내부 구현에 따라 다르겠지만, einsum을 사용한 경우 A[:, np.newaxis]처럼 임시 배열이 필요없기 때문에 훨씬 효율적이라고 할 수 있다.
<span style="color:gray">포스팅에 따르면 예시처럼 짧은 코드도 3배 가량 빨랐다고 한다.</span>

당연히 이 함수의 알파이자 오메가는 Einstein notation이다.

#### Einstein notation


