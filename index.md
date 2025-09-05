---
layout: default
title: Home
---

<p class="tagline">{{ site.description }}</p>

<ul class="post-list">
  {% for post in site.posts %}
  <li class="post-item">
    <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <div class="post-meta">{{ post.date | date: "%b %d, %Y" }}</div>
    <p class="excerpt">
      {% if post.excerpt %}
        {{ post.excerpt | strip_html | truncate: 140 }}
      {% else %}
        {{ post.content | strip_html | truncate: 100 }}
      {% endif %}
    </p>
  </li>
  {% endfor %}
</ul>