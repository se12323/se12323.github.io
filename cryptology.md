---
layout: articles
title: Cryptology
permalink: /cryptology.html
key: cryptology
cover:
articles:
    data_source: site.cryptology
    type: brief
    show_info: true
---

[//]: # (<ul>)

[//]: # (  {% for cryptology in site.cryptology %})

[//]: # (      <h2><a href="{{ cryptology.url }}">{{ cryptology.title }}</a></h2>)

[//]: # (  {% endfor %})

[//]: # (</ul>)

<ul>
{% for article in site.posts %}
  {% if article.categories contains 'cryptology' %}
      <h3><a href="{{ article.url }}">{{ article.title }}</a></h3> 
  {% endif %}
{% endfor %}
</ul>
