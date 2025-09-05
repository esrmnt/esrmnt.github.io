---
layout: default
title: Home
---

<h1 class="site-title">{{ site.title }}</h1>
<p class="tagline">{{ site.description }}</p>

<ul class="post-list">
  {% for post in site.posts %}
  <li class="post-item">
    <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <span class="post-meta">{{ post.date | date: "%b %d, %Y" }}</span>
    {% if post.excerpt %}<p class="excerpt">{{ post.excerpt | strip_html | truncate: 140 }}</p>{% endif %}
  </li>
  {% endfor %}
</ul>