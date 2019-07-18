---
layout: page
permalink: /machine_learning/
title: machine learning
description: How is it that machines learn?
---

<ul class="post-list">
{% for article in site.machine_learning reversed %}
    <li>
        <h2><a class="poem-title" href="{{ article.url | prepend: site.baseurl }}">{{ article.title }}</a></h2>
        <p class="post-meta">{{ article.date | date: '%B %-d, %Y — %H:%M' }}</p>
      </li>
{% endfor %}
</ul>