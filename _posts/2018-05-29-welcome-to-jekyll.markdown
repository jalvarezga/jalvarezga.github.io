---
layout: post
title:  "What was Bentkus trying to say!?"
date:   2023-05-29 18:05:55 +0300
image:  seyfettin-coffee-unsplash.jpg
tags:   Jekyll
---
<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>

<small>In honor to Vidmantas Bentkus.</small>



[comment]: <> (Useful link to integrate LaTeX to .md files https://docs.mathjax.org/en/v2.7-latest/tex.html)

[comment]: <> (Picture courtesy of unsplash, seyfettin dincturk, https://unsplash.com/photos/a-vase-of-flowers-on-a-counter-vzYixWSCqLM, https://unsplash.com/@dincturk)

### Context

In 2005 Vidmantas Bentkus introduced an innovative [probability concentration inequality](https://arxiv.org/abs/math/0410159). Astonishingly, this inequality has very practical applications in machine learning as shown by Angelopoulos, Bates et. al. in [2021](https://arxiv.org/abs/2110.01052).
However, the result is not easy to grasp at first glance. It uses unconventional notation across the whole paper.  Also, the proof can be unintuitive (it certainly was for me) when you don't have the author's background in probability theory. Here we will develop a self-contained proof of the Lemma 4.1 in Bentkus' original article.




#### Definition

Let $$n\mapsto p_n, \quad n \in \mathbb{Z}$$ be a function taking non-negative values. We say that the mapping is a log-concave function if and only if $$\begin{equation}p_{n+1}p_{n-1}\leq p_{n}^2\quad \forall n\in \mathbb{Z}\end{equation}$$.



#### Lemma
 Let $$p:\mathbb{Z}\longrightarrow [0,\infty)$$, $$q:\mathbb{Z}\longrightarrow [0,\infty)$$ be log-concave functions. Then the following functions are also log-concave:

(i) The convolution
$$(p*q)_{n}\overset{\triangle}{=}\sum\limits_{k=-\infty}^{\infty}p_{n-k}q_{k}$$.


(ii) $$n\mapsto t_n$$, where $$t_n\overset{\triangle}{=}\sum_{k\geq n}p_k$$.

(iii) Bernoulli probability mass functions.

(iv) Binomial survival functions (as discrete functions).

##### Proof

 We want to prove that $$(p*q)_{n-1}(p*q)_{n+1}\leq (p*q)_{n}^2,$$   

 which is equivalent to proving that $$\delta\geq 0$$, where $$\delta \overset{\triangle}{=}(p*q)_{n}^2-(p*q)_{n-1}(p*q)_{n+1}\geq 0$$. And $$\delta\geq 0\iff 2\delta\geq 0.$$

This last equivalence is useful since $$2\delta =\sum_{k,r=-\infty}^{\infty}\alpha\beta$$ with 


$$
\begin{equation*}
    \begin{split}
        &\alpha\overset{\triangle}{=} p_kp_r-p_{k+1}p_{r-1}\\
        &\beta\overset{\triangle}{=} q_{n-k}q_{n-r}-q_{n-k-1}q_{n-r+1}.
    \end{split}
\end{equation*}
$$


In order to prove this equality we develop the right side of the equation.


$$
\begin{equation*}
    \begin{split}
      \sum_{k,r=-\infty}^{\infty}\alpha\beta&=
      \sum_{k=-\infty}^{\infty}\sum_{r=-\infty}^{\infty}( p_kp_r-p_{k+1}p_{r-1})(q_{n-k}q_{n-r}-q_{n-k-1}q_{n-r+1})\\
      &=\sum_{k=-\infty}^{\infty}\sum_{r=-\infty}^{\infty}\Big\{ p_{k}p_{r}q_{n-k}q_{n-r}-p_{k}p_{r}q_{n-k-1}q_{n-r+1}\\
      &-p_{k+1}p_{r-1}q_{n-k}q_{n-r}+p_{k+1}p_{r-1}q_{n-k-1}q_{n-r+1}\Big\}\\
      &=\sum_{k=-\infty}^{\infty}\sum_{r=-\infty}^{\infty}p_{k}p_{r}q_{n-k}q_{n-r}-\sum_{k=-\infty}^{\infty}\sum_{r=-\infty}^{\infty}p_{k}p_{r}q_{n-k-1}q_{n-r+1}\\
      &-\sum_{k=-\infty}^{\infty}p_{k+1}q_{n-k}\sum_{r=-\infty}^{\infty}p_{r-1}q_{n-r}\\
      &+    \sum_{k=-\infty}^{\infty}\sum_{r=-\infty}^{\infty}p_{k+1}p_{r-1}q_{n-k-1}q_{n-r+1}  \\
      &=\underbrace{\sum_{k=-\infty}^{\infty}p_{k}q_{n-k}}_{S_1}\underbrace{\sum_{r=-\infty}^{\infty}p_{r}q_{n-r}}_{S_2}-\underbrace{\sum_{k=-\infty}^{\infty}p_{k}q_{n-k-1}}_{S_5\overset{\triangle}{=}}\underbrace{\sum_{r=-\infty}^{\infty}p_{r}q_{n-r+1}}_{S_6}\\
      &-\underbrace{\sum_{k=-\infty}^{\infty}p_{k+1}q_{n-k}}_{S_7}\underbrace{\sum_{r=-\infty}^{\infty}p_{r-1}q_{n-r}}_{S_8}\\
      &+ 
\underbrace{\sum_{k=-\infty}^{\infty}p_{k+1}q_{n-k-1}}_{S_3\overset{\triangle}{=}} \underbrace{\sum_{r=-\infty}^{\infty}p_{r-1}q_{n-r+1}}_{S_4\overset{\triangle}{=} }\\
&=(\#).
\end{split}
\end{equation*}
$$



With changes of variable, we can prove that $$S_1=S_2=S_3=S_4=(p*q)_{n}$$. For example, by setting $$t=t(k)\overset{\triangle}{=} n-k$$, we get that $$S_1=\sum_{t=-\infty}^\infty p_{n-t}q_t=(p*q)_{n}$$. For $$S_3$$, we can consider $$t=t(k)=n-k-1$$, and rewrite $$S_3\overset{\triangle}{=} \sum_{k=-\infty}^{\infty}p_{k+1}q_{n-k-1}=\sum_{t=-\infty}^{\infty}p_{n-t}q_t=(p*q)_{n}$$, and apply analogous ideas for $$S_2$$ and $$S_4$$. Moreover, we can prove that $$S_5S_6=S_7S_8=\sum_{k=-\infty}^{\infty}p_{n-1-k}q_{k}\sum_{k=-\infty}^{\infty}p_{n+1-k}q_{k}$$
making an analogous change of variables for each series.



Hence $$(\#)=2((p*q)_{n})^2-2\sum_{k=-\infty}^{\infty}p_{n-1-k}q_{k}\sum_{k=-\infty}^{\infty}p_{n+1-k}q_{k}$$

On the other hand, we have that 

$$
\begin{equation*}
    \begin{split}
      2\delta&=2\{(p*q)_{n}^2-(p*q)_{n-1}(p*q)_{n+1} \}  \\  
      &=2\{ \big(\sum_{k=-\infty}^{\infty}p_{n-k}q_{k} \big)^2 -(\sum_{k=-\infty}^{\infty}p_{n-1-k}q_{k})(\sum_{k=-\infty}^{\infty}p_{n+1-k}q_{k}) \}.
    \end{split}
\end{equation*}
$$


So $$2\delta =\sum_{k,r=-\infty}^{\infty}\alpha\beta$$.

Recalling that we want to prove that $$\delta\geq 0$$, we study 2 cases.

Case $$1$$: $$k\geq r$$.

We know that $$p_{n+1}p_{n-1}\leq p_{n}^2 \quad \forall n\in \mathbb{Z}$$. This implies that $$p_{k+1}p_{r-1}\leq p_{k}p_{r}\quad \forall r\in \mathbb{Z}, \quad \forall k\in \{ r,r+1, \dots\}$$.
In order to notice why this is true, suppose without loss of generality that the involved quantities are strictly positive in order to avoid dividing by zero. Then



$$\begin{equation*}p_{k+1}p_{r-1}\leq p_{k}p_{r}\iff \frac{p_{r-1}}{p_r}\leq \frac{p_{k}}{p_{k+1}}.\end{equation*}$$

In terms of fractions, our hypothesis states that $$\frac{p_{k-1}}{p_k}\leq \frac{p_{k}}{p_{k+1}}$$. Hence  applying the hypothesis as many times as needed (a finite number of times) $$\frac{p_{r-1}}{p_{r}}\leq \frac{p_{r}}{p_{r+1}} \leq\dots \leq \frac{p_{k-2}}{p_{k-1}}\leq \frac{p_{k-1}}{p_{k}}\leq \frac{p_{k}}{p_{k+1}}$$ leading to the result. The exact same ideas can be applied to $$n\mapsto q_n$$ by the hypothesis that the mapping is also log-concave.



Now with that result in mind and using the definitions of $$\alpha$$ and $$\beta$$ we can  conclude that the following implication is true


$$\begin{equation*}k \geq r \implies \alpha,\beta\geq 0 \end{equation*}$$

Hence  $$k \geq r \implies \alpha\beta\geq 0 $$.



Case 2: $$k<r$$.

By the above argument (Case 1), we know that $$k\begin{equation*}\geq r\implies p_{k+1}p_{r-1}\leq p_{k}p_{r}\quad \forall r\in \mathbb{Z}, \quad \forall k\in \{ r,r+1, \dots\}\end{equation*}$$

Which lead to $$\begin{equation*}k\geq r  \implies \alpha, \beta \geq 0\end{equation*}.$$

Now switching the roles of $$r$$ and $$k$$ in that argument, we get that
$$k<r\implies[ \alpha\leq 0 \quad \& \quad \beta\leq 0]$$ Thus,
$$k<r\implies \alpha\beta\geq0$$
By cases 1 and 2, $$2\delta=\sum_{k,r=-\infty}^{\infty}\alpha\beta\geq0$$, because $$2\delta$$ is just a series in which the terms are always non-negative. Therefore $$\delta\geq 0$$.


Next we prove (ii). We are going to prove that $$t_{n-1}t_{n+1}\leq t_{n}^2\quad \forall n\in \mathbb{Z}$$.
First, since $$n\mapsto p_n$$ is log-concave, $$p_n\geq 0\forall n\in \mathbb{Z}$$. Thus $$t_n\overset{\triangle}{=}\sum_{k\geq n}p_k\geq 0\forall n\in \mathbb{Z}$$.
Define $$w_n\overset{\triangle}{=} I\{ n\leq0\}, \quad\forall n\in \mathbb{Z}$$.

We claim that $$n \mapsto w_n$$ is a log-concave function: clearly, $$w_n\geq 0\forall n\in \mathbb{Z}$$, since $$w_n \in \{ 0,1\}$$. Moreover, $$w_{n-1}w_{n+1} \leq  w_{n}^2 \forall n\in \mathbb{Z}$$.
This is verified by cases.

Let $$n\in \mathbb{Z}$$ be an arbitrary integer.


Case a: $$n\leq0$$. Then by definition of the indicator function, $$w_n=1$$ and by definition of the mapping $$n\mapsto w_n$$, 

$$w_{n-1 }w_{n+1} \leq 1 =w_{n}^2$$.


Case b: $$n>0$$. Then by definition, $$w_n=0$$, but since $$n>0$$, then $$n+1>0$$, so $$w_{n+1}=0$$
 and we get $$w_{n-1 }w_{n+1} \leq 0 =w_{n}^2$$, since we have an inequality of the form $$ 0\leq 0$$, which trivially holds.

So now we have that $$w_n$$ is a log concave function, and by the hypothesis of the Lemma, $$p_n$$ is a log-concave function. Next we will prove that actually, $$t_n=(p*w)_n$$. Let $$n\in \mathbb{Z}$$ be an arbitrary integer.

Then 

$$
\begin{equation*}
    \begin{split}
     (p*w)_n&=\sum_{k=-\infty}^{\infty}p_{n-k}w_k\\
     &= \sum_{k=-\infty}^{\infty}p_{n-k} I \{k\leq0\}\\
     &=\sum_{k=-\infty}^{0} p_{n-k}\\
     &=\sum_{k\geq n}p_k\\
     &=t_n
    \end{split}
\end{equation*}
$$

By (i), we conclude that $$n\mapsto t_n\overset{\triangle}{=}\sum_{k\geq n}p_k$$ is log-concave.



Now we prove (iii). Let $$X\sim Bernoulli(p),\quad p\in (0,1)$$. Then its probability mass function is given by $$f_X(x)=p^{x}(1-p)^{1-x}\mathbb{I}_{\{0,1\}}(x)$$.
Clearly, $$f_X(x)\geq 0\quad \forall x\in \mathbb{R}$$, in particular in $$\mathbb{Z}$$.

It is easy to verify that $$f_X(x-1)f_X(x+1)\leq f_X(x)^2\quad \forall x\in \mathbb{Z}$$ by cases, in a similar fashion as the one previously done.

Hence the probability mass function of a Bernoulli random variable is log-concave.

Next we prove (iv).
First we prove that as a consequence of (i) and (iii), Binomial probability mass functions are log-concave.
That is, if $$X_m\sim Bin(m,p)$$, then $$f_{X_m}(x)= \binom{m}{x}p^{x}(1-p)^{m-x}I_{\{0,1,\dots, m\}}(x)$$ is a log-concave function for each $$m\in \mathbb{N}$$. 
The proof is done by induction on $$m$$.

The basis of the induction ($$m=1$$) follows from the fact that a Binomial distribution with $$m=1$$ is a Bernoulli distribution.
Since we are considering the log concave functions as functions in $$\mathbb{Z}$$, we will adopt the following notation for the probability mass functions as restricted to $$\mathbb{Z}$$: $$t_x\overset{\triangle}{=} f_{X_m}(x)$$.

$$m=2$$

We claim that $$t_n=(z*w)_n\quad \forall n\in \mathbb{Z}$$, where $$z$$ and $$w$$ are Bernoulli probability mass functions. 

$$t_x=\binom{2}{x}p^x(1-p)^{2-x}I_{\{0,1,2\}}(x)$$ so 

$$t_0=(1-p)^2, \quad t_1=2p(1-p) , \quad t_2=p^2.$$

And 

$$\begin{equation}w_k=p I\{k=1\}+(1-p)I\{k=0\},\end{equation}$$

$$\begin{equation}z_k=pI\{k=1\}+(1-p)I\{k=0 \}.\end{equation}$$

So,

$$(z*w)_{0}=\sum_{k=-\infty}^{\infty}z_{0-k}w_k=z_0w_0=(1-p)^2=t_0$$

$$(z*w)_{1}=\sum_{k=-\infty}^{\infty}z_{1-k}w_k=z_1w_0+z_0w_1=2p(1-p)=t_1$$


$$(z*w)_{2}=\sum_{k=-\infty}^{\infty}z_{2-k}w_k=z_1w_1=p^2=t_2$$


$$(z*w)_n=t_n=0\quad\forall n\in \mathbb{Z}-\{0,1,2\}$$

$$\underline{Hypothesis of induction}$$: $$Bin(m,p)$$ is log concave for any $$p\in (0,1)$$, and some $$m\in \mathbb{N}$$.

We will prove that $$Bin(m+1,p)$$  mass probability function is also log concave for any $$p\in (0,1)$$.


Denote $$t$$ the probability mass function of a $$Bin(m+1,p)$$ random variable, $$w$$ the density of a Bernoulli random variable and $$z$$ the density of a $$Bin(m,p)$$ random variable, which by our basis of induction and our hypothesis of induction, respectively, both functions are log-concave. 
Now, we are going to prove that $$t=(z*w)$$.

Let $$x\in \{0,1, \dots, m+1\}$$. Then 

$$
\begin{equation*}
    \begin{split}
       (z*w)_x&= \sum_{k=-\infty}^{\infty}z_{x-k}w_k\\
       &=z_{x}w_{0}+z_{x-1}w_1\\
       &=\binom{m}{x}p^x(1-p)^{m-x}(1-p)+\binom{m}{x-1}p^{x-1}(1-p)^{m-x+1}p\\
       &=p^{x}(1-p)^{m-x+1}\Big\{ \binom{m}{x} +\binom{m}{x-1}\Big\}\\
       &=p^{x}(1-p)^{m+1-x}\binom{m+1}{x}
    \end{split}
\end{equation*}
$$

since  $$\binom{m}{x} +\binom{m}{x-1}=\binom{m+1}{x}\forall x\in \{0,1\dots, m+1\}$$

$$(z*w)_x=0=t_x\forall x\in \mathbb{Z}-\{0,1,\dots, m+1\}.$$


Finally, once that we have that Binomial probability mass functions are log concave, we apply (ii) to conclude that the Binomial survival function is log concave, and conclude the proof.$$\blacksquare$$


