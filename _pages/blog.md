---
layout: page
title: Blog
permalink: /blog/
---

## Blog posts

{% for post in site.categories.blog %}
  {% include article-content.html %}
{% endfor %}

## Undergrad projects

{% for post in site.categories.undergrad %}
  {% include article-content.html %}
{% endfor %}