---
layout: articles
title: Algorithm
permalink: /algorithm.html
key: algorithm
cover:
articles:
    data_source: site.algorithm
    type: brief
    show_info: true
---

[//]: # (<ul>)

[//]: # (  {% for algo in site.algorithm %})

[//]: # (      <h2><a href="{{ algo.url }}">{{ algo.title }}</a></h2>)

[//]: # (  {% endfor %})

[//]: # (</ul>)

<ul>
{% for article in site.posts %}
  {% if article.categories contains 'algorithm' %}
      <h3><a href="{{ article.url }}">{{ article.title }}</a></h3> 
  {% endif %}
{% endfor %}
</ul>
