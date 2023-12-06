---
layout: post
title:  "What was Bentkus trying to say!?"
date:   2023-05-29 18:05:55 +0300
image:  10.jpg
tags:   Jekyll
---
<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>
In 2005 Vidmantas Bentkus an innovative [concentration inequality](https://arxiv.org/abs/math/0410159). Astonishingly, this inequality has very practical implications in machine learning as shown by Angelopoulos, Bates et. al. in [Learn then Test](https://arxiv.org/abs/2110.01052).
However, the result is not easy to wrap at first glance.  Also, the proof is quite unintuitive. Here we will develop a self-contained proof working in an i.d.d. setting, which is a little bit more conservative than Bentkus' original result.




We add code to get mathjax and support to integrate LaTeX within .md files. 
Interacting with LaTeX $$\alpha, \beta$$. 


$$\frac{a}{b}$$
$$\pi\approx 3.1415$$




$$\mathbb{P}\Big(X=x\Big)$$.


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
