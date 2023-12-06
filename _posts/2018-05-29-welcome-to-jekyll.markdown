---
layout: post
title:  "What was Bentkus trying to say!?"
date:   2023-05-29 18:05:55 +0300
image:  tyler-nix-coffee-unsplash.jpg
tags:   Jekyll
---
<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>

<small>In honor to Vidmantas Bentkus.</small>


[comment]: <> (Picture courtesy of unsplash,Tyler Nix, https://unsplash.com/photos/person-pouring-liquid-on-drinking-glass-yKalliZTaQU)


In 2005 Vidmantas Bentkus an innovative [concentration inequality](https://arxiv.org/abs/math/0410159). Astonishingly, this inequality has very practical implications in machine learning as shown by Angelopoulos, Bates et. al. in [Learn then Test](https://arxiv.org/abs/2110.01052).
However, the result is not easy to grasp at first glance.  Also, the proof is quite unintuitive. Here we will develop a self-contained proof working in an i.d.d. setting, which is a little bit more conservative than Bentkus' original result.




We add code to get mathjax and support to integrate LaTeX within .md files. 
Interacting with LaTeX $$\alpha, \beta$$. 


$$\frac{a}{b}$$
$$\pi\approx 3.1415$$




$$\mathbb{P}\Big(X=x\Big)$$.


### Setting and notation

In this section we will explore the construction of a rejection region based on a test statistic originated form Bentkus' celebrated theorem from 2004. The emphasis is on giving accessible, yet rigorous arguments that lead to the proposed test statistic from LTT (2021). We will dive into a proof of the  Bentkus inequality, with some slight modifications, making arguments as self-contained as possible.

Let $$X_1,X_2,\dots, X_n$$ be the differences of a martingale defined by $$M_n\coloneqq \sum_{i=1}^{n}X_i$$ and suppose that each satisfy the boundedness condition

 $$\mathbb{P}\{-p_k\leq X_k \leq 1-p_k \}, \quad k\in \{1, \dots, n \}, $$


where $$0\leq p_k\leq 1 \quad \forall k \in \{1,\dots, n \}$$ is non-random.



#### Definition

Let $$b\in \mathbb{R} -  \{0\}$ and $\sigma>0$$. We say that a random variable $$\epsilon=\epsilon(\sigma^2,b)$$ is a Bernoulli random variable if it takes at most two possible  real values, and satisfies the following conditions:

$$\Prob\{\epsilon= b\}=\frac{\sigma^2}{\sigma^2+b^2}\quad \Prob\Big\{ \epsilon=\frac{-\sigma^2}{b}\Big\}=\frac{b^2}{b^2+\sigma^2}$$






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
