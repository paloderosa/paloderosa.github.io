---
layout: page
permalink: /machine_learning/
title: machine learning
description: Showcase your writing, short stories, or poems. Replace this text with your description.
---

<ul class="post-list">
{% for poem in site.machine_learning reversed %}
    <li>
        <h2><a class="poem-title" href="{{ poem.url | prepend: site.baseurl }}">{{ poem.title }}</a></h2>
        <p class="post-meta">{{ poem.date | date: '%B %-d, %Y — %H:%M' }}</p>
      </li>
{% endfor %}
</ul>