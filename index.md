---
layout: default
title: Home
---

<p class="tagline">{{ site.description }}</p>

{% assign tags = site.posts | map: 'tags' | join: ',' | split: ',' | uniq | sort %}
{% for tag in tags %}
  {% if tag != '' %}
    <h2 class="tag-heading">{{ tag | capitalize }}</h2>
    <ul class="post-list">
      {% for post in site.posts %}
        {% if post.tags contains tag %}
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
        {% endif %}
      {% endfor %}
    </ul>
  {% endif %}
{% endfor %}