---
layout: post
title:  "What was Bentkus trying to say!?"
date:   2023-05-29 18:05:55 +0300
image:  louis-hansel-coffee-unsplash.jpg
tags:   Jekyll
---
<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>

<small>In honor to Vidmantas Bentkus.</small>



[comment]: <> (Useful link to integrate LaTeX to .md files https://docs.mathjax.org/en/v2.7-latest/tex.html)

[comment]: <> (Picture courtesy of unsplash, Louis Hansel, https://unsplash.com/photos/stainless-steel-espresso-machine-on-brown-wooden-table-9v3nL6pAxjw)


In 2005 Vidmantas Bentkus introduced an innovative [concentration inequality](https://arxiv.org/abs/math/0410159). Astonishingly, this inequality has very practical implications in machine learning as shown by Angelopoulos, Bates et. al. in [Learn then Test](https://arxiv.org/abs/2110.01052).
However, the result is not easy to grasp at first glance.  Also, the proof can be unintuitive (it certainly was for me) when you don't have the author's background in probability theory. Here we will develop a self-contained proof working in an i.d.d. setting, which is a little bit more conservative assumption than Bentkus' original result.




We add code to get mathjax and support to integrate LaTeX within .md files. 
Interacting with LaTeX $$\alpha, \beta$$. 


$$\frac{a}{b}$$
$$\pi\approx 3.1415$$




$$\mathbb{P}\Big(X=x\Big)$$.


### Setting and notation

In this section we will explore the construction of a rejection region based on a test statistic originated form Bentkus' celebrated theorem from 2004. The emphasis is on giving accessible, yet rigorous arguments that lead to the proposed test statistic from LTT (2021). We will dive into a proof of the  Bentkus inequality, with some slight modifications, making arguments as self-contained as possible.

Let $$X_1,X_2,\dots, X_n$$ be the differences of a martingale defined by $$M_n\overset{\triangle}{=} \sum\limits_{i=1}^{n}X_i$$ and suppose that each satisfy the boundedness condition

 $$\mathbb{P}\{-p_k\leq X_k \leq 1-p_k \}, \quad k\in \{1, \dots, n \}, $$


where $$0\leq p_k\leq 1 $$  is non-random  $$\forall k \in \{1,\dots, n \}$$.



#### Definition

Let $$b\in \mathbb{R} -  \{0\}$$ and $$\sigma>0$$. We say that a random variable $$\epsilon=\epsilon(\sigma^2,b)$$ is a Bernoulli random variable if it takes at most two possible  real values, and satisfies the following conditions:

$$\begin{equation} \mathbb{P}\{\epsilon= b\}=\frac{\sigma^2}{\sigma^2+b^2}, \quad \mathbb{P}\Big\{ \epsilon=\frac{-\sigma^2}{b}\Big\}=\frac{b^2}{b^2+\sigma^2} \end{equation}.$$




As a consequence, it follows that if $$\epsilon=\epsilon(\sigma^2, b)$$ is a Bernoulli random variable, then $$\mathbb{E}(\epsilon)=0$$ and $$\mathbb{V}(\epsilon)=\sigma^2$$. This is a slightly different definition from the usual definition of a Bernoulli random variable where the two possible values that the random variable takes are $$0$$ and $$1$$. We will deviate from the usual definition in some situations as we prove Benkus' Inequality.


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
&=(\#),
\end{split}
\end{equation*}
$$
with

$$S_1\overset{\triangle}{=}$$



$$\blacksquare$$




You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
