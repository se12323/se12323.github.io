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

<ul>
  {% for author in site.algorithm %}
      <h2><a href="{{ algorithm.url }}">{{ algorithm.title }}</a></h2>
  {% endfor %}
</ul>

