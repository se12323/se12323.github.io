---
layout: articles
title: C++
permalink: /cpp.html
key: cpp
cover:
articles:
    data_source: site.cpp
    type: brief
    show_info: true
---

[//]: # (<ul>)

[//]: # (  {% for cpp in site.cpp %})

[//]: # (      <h2><a href="{{ cpp.url }}">{{ cpp.title }}</a></h2>)

[//]: # (  {% endfor %})

[//]: # (</ul>)

<ul>
{% for article in site.posts %}
  {% if article.categories contains 'cpp' %}
      <h3><a href="{{ article.url }}">{{ article.title }}</a></h3> 
  {% endif %}
{% endfor %}
</ul>
