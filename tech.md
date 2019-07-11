---
layout: page
permalink: /tech/
title: machine learning
description: Building things with code
---

<ul class="post-list">
{% for article in site.tech reversed %}
    <li>
        <h2><a class="poem-title" href="{{ poem.url | prepend: site.baseurl }}">{{ article.title }}</a></h2>
        <p class="post-meta">{{ article.date | date: '%B %-d, %Y — %H:%M' }}</p>
      </li>
{% endfor %}
</ul>