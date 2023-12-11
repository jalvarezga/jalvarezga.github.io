---
layout: post
title:  Simulation with the Bootstrap
date:   2022-06-19 15:01:35 +0300
image:  violinPlot.png
tags:   Art
author: Joaquin
---
<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>


## The context of what we are doing to do

The purpose is to illustrate the Bootstrap through an example. This is a very powerful and useful technique with many applications. In order to develop the idea behind the method, we are going to make use of a motivation presented in the [ISLR](https://www.statlearning.com) book. 

Suppose we want to invest in two different stocks in the market. We have access to historical data of the daily returns (joint returns) of those two assets, $$(X_i,Y_i) \stackrel{i.i.d.}{\sim} \mathbb{P}_{X,Y},\quad i=1,\dots,n$$. $$\mathbb{P}_{X,Y}$$ denotes a joint probability distribution. For simplicity we assume these observations are independent, however, we could make more relaxed assumptions (or use a more sophisticated Time Series Model) and Bootstrap still provides the magic. We are going to allocate a proportion of $\alpha\in (0,1)$ of our total money we want to invest to the stock X and the rest ($1-\alpha$) to asset Y. We want to make the allocation in such a way that we minimize the variance of the return of the portfolio.

In this context, the total return in terms of the proportion we invest to each asset is given by $$f(\alpha, X, Y):= \alpha X+(1-\alpha)Y, \quad \forall \alpha \in (0,1)$$ , where $$(X,Y) \sim \mathbb{P}_{X,Y}$$ is an observation of the daily joint returns of the asset. We want to minimize $$\mathbb{V}ar(f(\alpha, X, Y))$$ with respect to alpha, picking the $$\alpha \in (0,1)$$ that minimizes that expression. That is, we want to minimize the  variance of the daily return of a portfolio consisting of two assets, with daily returns for each asset denoted by X and Y, respectively. We use the following notation: $$\sigma_X^2 := \mathbb{V}(X),\quad \sigma_Y^2:=\mathbb{V}ar(Y), \quad \sigma_{X,Y}:=Cov(X,Y)$$. We assume that we $$\underline{don't}$$ know this quantities, and we assume that they exist.



Notice that $$\mathbb{V}ar(f(\alpha, X, Y))=\mathbb{V}(\alpha X+(1-\alpha)Y)= \alpha^2\mathbb{V}(X)+(1-\alpha)^2\mathbb{V}(Y)+2\alpha(1-\alpha)Cov(X,Y)= \alpha^2\sigma_X^2+(1-\alpha)^2\sigma_Y^2+2\alpha(1-\alpha)\sigma_{X,Y}$$ is a polynomial in $$\alpha$$. We can use simple calculus to verify that 


$$\begin{equation}\alpha^*:=\frac{\sigma_Y^2-\sigma_{X,Y}}{\sigma_X^2+\sigma_Y^2-2\sigma_{X,Y}}\end{equation}$$


is a global minimum of $$F(\alpha):=\mathbb{V}ar(f(\alpha, X, Y))$$.  Now, given that $$\sigma_X^2, \sigma_Y^2$$ and $$\sigma_{X,Y}$$ are unknown quantities, we can construct a plug-in estimator of $$\alpha^*$$, denoted by $$\widehat{\alpha^*}$$,
using the data and the unbiased estimators of $$\sigma_X^2, \sigma_Y^2$$ and $$\sigma_{X,Y}$$, denoted by $$\widehat{\sigma_X^2}, \widehat{\sigma_Y^2}, \widehat{\sigma_{X,Y}}$$ and get:

$$\begin{equation}\widehat{\alpha^*}:=\frac{\widehat{\sigma_Y^2}-\widehat{\sigma_{X,Y}}}{\widehat{\sigma_X^2}+\widehat{\sigma_Y^2}-2\widehat{\sigma_{X,Y}}}\end{equation}.$$




Our objective is to  know (or in statistical terms, to estimate)  $$\alpha^*$$, and we are going to do that through $$\widehat{\alpha^*}$$ and the available data.

## Theory: we have access to a data generator

We first generate some data.


{% highlight r %}
alphas=rep(0,1000)# to store the data
set.seed(1)#set a seed to keep reproducibility
mu=c(0.3,0.9) #average daily returns
Sigma=matrix(c(2,-2,-2,4), nrow=2,  byrow = T) #positive definite matrix
mu
Sigma
library(MASS) #we load a library to generate samples from a multivariate normal distribution
returns=mvrnorm(n = 100, mu, Sigma) #simulate 100 observations of a bivariate normal.
#we plot the resulting generated samples
plot(returns, xlab = 'X',ylab='Y', main='Joint Returns', col='red', pch=16)
#the scatter plot of the data  suggests a mean near (0.3,0.9), the center of the elipse and a negative correlation between the variables, since the principal axis of the elipse has a negative slope.
{% endhighlight %}




{% highlight R %}
for(j in 1:1000){
  set.seed(j) # to conserve reproducibility of our results
  returns=mvrnorm(n = 100, mu, Sigma) #we generate a random sample
  sigx=var(returns[,1])
  sigy=var(returns[,2])
  covxy=cov(returns[,1],returns[,2])
  alpha=(sigy-covxy)/(sigx+sigy-2*covxy)
  alphas[j]=alpha
  
}
{% endhighlight %}



