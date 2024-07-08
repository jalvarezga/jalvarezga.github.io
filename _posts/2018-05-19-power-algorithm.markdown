---
layout: post
title:  Power iteration algorithm
date:   2021-01-19 15:01:35 +0300
image:  09.jpg
tags:   Blog
author: Joaquin
---

<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>


## By courtesy of [Juan Carlos Aguilar](https://facultad.itam.mx/en/facultad/juan-carlos-aguilar-villegas) 's Numerical Calculus course at ITAM.

This is the first project that I did using LaTeX! I find LaTeX to be a beautiful and elegant form of writting scientific articles. The power iteration algorithm is one of the algorithms that I enjoyed most during my undergraduate studies. I believe that it is elegant and simple. Let us describe the algorithm with an adequate context and an argument showing what it does and why it works.




#### Definitions and context.

Dominant eigenvalue of a matrix:  Let $$A\in \mathbb{R}^{n\times n}$$ be a diagonalizable matrix over $$\mathbb{C}$$, and $$\lambda_{1},\lambda_{2},\dots,\lambda_{n}\in \mathbb{C}$$ be its corresponding eigenvalues.
$$\lambda_{j}$$ is the dominant eigenvalue of A if and only if

$$|\lambda_{i}|\leq |\lambda_{j}|, \text{ for all } i=1,2,\dots,n.$$ 

##### Remark:
we will assume that we have a matrix $$A$$,which is diagonalizable. Hence, without loss of generality, let´s suppose that $$\lambda_{1}$$ is a dominant eigenvalue for our diagonalizable matrix A.

We say that $$\lambda_{1}$$ is the only dominant eigenvalue of A if and only if
$$|\lambda_{1}|>|\lambda_{j}| \text{ for all } j=2,\dots,n.$$




### Approximation to the (only) dominant eigenvalue of a real squared matrix (if it exists)


In this section we´ll discuss the power iteration algorithm focusing in $$\mathbb{R}$$, however, the ideas can be extended to $$\mathbb{C}$$.


Let $$A\in \mathbb{R}^{n\times n}$$ be a diagonalizable matrix over $$\mathbb{R}$$ and $$\lambda_{1},\lambda_{2},...,\lambda_{n}\in\mathbb{R}$$ be the corresponding eigenvalues.

Suppose that $$\lambda_{1}$$ is the only dominant eigenvalue of A. Furthermore, without loss of generality we can write:
$$|\lambda_{1}|>|\lambda_{2}|\geq|\lambda_{3}|\geq\dots\geq|\lambda_{n}|.$$



Since $$A$$ is diagonalizable in $$\mathbb{R}$$, there exist linearly independent eigenvectors of $$A$$,
$$\vec{v_{1}}, \vec{v_{2}},\dots,\vec{v_{n}} \in \mathbb{R}^{n}$$, corresponding to the eigenvalues

$$\lambda_{1},\lambda_{2},...,\lambda_{n}$$, respectively and form a basis of $$\mathbb{R}^{n}$$.



Let $$\vec{u_{0}}\in\mathbb{R}^{n}-\{\vec{0}\}$$ be an arbitrary vector.



Since $$\{\vec{v_{1}},\dots,\vec{v_{n}}\}$$ is a basis of $$\mathbb{R}^{n}$$, there exist constants  $$\alpha_{1},\alpha_{1},\dots,\alpha_{n} \in \mathbb{R}$$
such that:


$$
\begin{equation}
    \vec{u_{0}}=  \sum_{i = 1}^n\alpha_{i}\vec{v_{i}}.
\end{equation}
$$



Multiplying both sides by $$A$$:

$$\begin{equation}
A\vec{u_{0}}=  A\sum_{i = 1}^n\alpha_{i}\vec{v_{i}}
=\sum_{i = 1}^n\alpha_{i}A\vec{v_{i}}.
\end{equation}$$


And since $$\vec{v_{i}}$$ is an eigenvector of $$A$$ corresponding to the eigenvalue  $$\lambda_{i}$$, then by definition of eigenvector we get:

$$\begin{equation}
A\vec{u_{0}}=  \sum_{i = 1}^n\alpha_{i}\lambda_{i}\vec{v_{i}}.
\end{equation}$$


Again, multiplying by $$A$$ in both sides, using the same argument as above we get:
$$\begin{equation}
A^2\vec{u_{0}}=  \sum_{i = 1}^n\alpha_{i}\lambda_{i}^2\vec{v_{i}}.
\end{equation}$$




Proceeding by induction, we get:

$$\begin{equation}
A^k\vec{u_{0}}=  \sum_{i = 1}^n\alpha_{i}\lambda_{i}^k\vec{v_{i}}
=\alpha_{1}\lambda_{1}^k\vec{v_{1}}+\alpha_{2}\lambda_{2}^k\vec{v_{2}}+\dots +\alpha_{n}\lambda_{n}^k\vec{v_{n}},
\end{equation}$$

for all $$k \in\mathbb{N}$$.




Dividing both sides by $$\lambda_{1}^k$$ (remember that $$\lambda_{1}$$ is the only dominant eigenvalue of A by hypothesis):

$$
\begin{equation}
\frac{1}{\lambda_{1}^k}A^k\vec{u_{0}}=\alpha_{1}\vec{v_{1}}+\alpha_{2}\left(\frac{\lambda_{2}}{\lambda_{1}}\right)^k\vec{v_{2}}+\dots+\alpha_{n}\left(\frac{\lambda_{n}}{\lambda_{1}}\right)^k\vec{v_{n}}.
\end{equation}$$




And since $$
0\leq|\lambda_{n}|\leq|\lambda_{n-1}|\leq\dots\leq|\lambda_{2}|<|\lambda_{1}|$$, then dividing all the inequalities by $$|\lambda_{1}|>0$$, we get that 
$$0\leq\left|\frac{\lambda_{n}}{\lambda_{1}}\right|\leq\left|\frac{\lambda_{n-1}}{\lambda_{1}}\right|\leq\dots\leq\left|\frac{\lambda_{2}}{\lambda_{1}}\right|<1,$$


if and only if
$$0\leq\bigl\vert\frac{\lambda_{n}}{\lambda_{1}}\bigl\vert^k\leq\bigl\vert\frac{\lambda_{n-1}}{\lambda_{1}}\bigl\vert^k\leq\dots\leq\bigl\vert\frac{\lambda_{2}}{\lambda_{1}}\bigl\vert^k<1 \text{ for all }  k\in\mathbb{N}.$$


Therefore 


$$\begin{equation} \lim_{k\to\infty}{\Big(\frac{\lambda_{j}}{\lambda_{1}}\Big)^k}=0, \text{ for } j\in\{ 2,3,\dots,n\} .\end{equation}$$





Going back to the equation that we obtain by induction, and taking limits in both sides we have that:

$$
\begin{equation}
 \lim_{k\to\infty}\frac{1}{\lambda_{1}^k}A^k\vec{u_{0}}=\lim_{k\to\infty}\alpha_{1}\vec{v_{1}}+\alpha_{2}\left(\frac{\lambda_{2}}{\lambda_{1}}\right)^k\vec{v_{2}}+\dots+\alpha_{n}\left(\frac{\lambda_{n}}{\lambda_{1}}\right)^k\vec{v_{n}}.
\end{equation}$$


Using the fact that $$\lambda_1$$ is a dominant eigenvalue, in the limit, this equation simplifies to:


$$\begin{equation}
 \lim_{k\to\infty}\frac{1}{\lambda_{1}^k}A^k\vec{u_{0}}=\alpha_{1}\vec{v_{1}}.
\end{equation}$$




 This suggests that for a big $$k \in \mathbb{N}$$ we obtain the following approximation:
$$\begin{equation}
\frac{1}{\lambda_{1}^k}A^k\vec{u_{0}}\approx\alpha_{1}\vec{v_{1}}.
\end{equation}$$

Here it is worth to pause and make a couple of observations:


1. We picked $$\vec{u_{0}}$$ to be an arbitrary vector in $$\mathbb{R}^{n}$$. However, $$\vec{u_{0}}$$ needs to satisfy that $$\alpha_{1}$$ is different form 0 so that the last approximation is different from $$\vec{0}$$, since $$\vec{0}$$ is not an eigenvector by definition.



2. The hole point of all the argument above is to motivate an algorithm that approximates the only dominant eigenvalue of A (i.e.$$\lambda_{1}$$), which we don´t know a priori and actually want to approximate, assuming that it exists.


3. A useful property of eigenvectors worth to recall:
Let $$A\in\mathbb{R}^{n\times n}$$ and suppose that $$\vec{v_{1}}\in\mathbb{R}^{n}$$ is an eigenvector of $$A$$, then $$\alpha\vec{v_{1}}$$ is also an eigenvector of A for all $$\alpha\in \mathbb{R}-\{0\}$$. Moreover, from the proof of this statement it follows that $$\vec{v_{1}}$$ and $$\alpha\vec{v_{1}}$$ have the same associated eigenvalue of $$A$$.
Considering the last remark, $$\frac{A^k\vec{u_{0}}}{||A^k\vec{u_{0}||}}$$ is parallel to 
$$\frac{1}{\lambda_{1}^k}A^k\vec{u_{0}}$$ (given that we are just scaling the vector $$A^k\vec{u_{0}}$$)
and thus $$\frac{A^k\vec{u_{0}}}{||A^k\vec{u_{0}||}}$$ tends to an eigenvector of A associated to the dominant eigenvalue $$\lambda_{1}$$ as $$k\xrightarrow{}\infty$$.






## Power iteration algorithm: a pseudocode

#### Inputs: $$A$$, $$\vec{u_{0}}$$, $$maxNumIter$$, $$Tol$$.

#### Output: $$\ell_{k}$$, $$\vec{u}_{k}$$.



1.- $$k \leftarrow 1$$

2.- $$\textbf{While } k<maxNumIter:$$

3.- $$\vec{u_{k}} \leftarrow$$ $$\frac{A\vec{u}_{k-1}}{\text{norm}(A\vec{u}_{k-1})}$$

4.- $$\ell_{k}\leftarrow \vec{u}_{k}^T A\vec{u}_{k}$$

5.- $$\textbf{If } \frac{\text{norm}(A\vec{u}_{k}-\ell_{k}\vec{u}_{k})}{\text{norm}(A\vec{u_{k}})}\leq Tol: \textbf{ Break while}$$

6.- $$\textbf{Else:}$$

7.- $$k\leftarrow k+1$$

8.- $$\textbf{End if}$$ 

9.- $$\textbf{End while}$$

10.- $$\textbf{Return } \ell_{k},\vec{u}_{k}.$$

Where $$\text{norm}()$$ denotes the Euclidean norm function for vectors in $$\mathbb{R}^n$$. Notice that the initial $$\vec{u_{0}}$$ must satisfy $$A\vec{u_{0}}\neq\vec{0}$$.
