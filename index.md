---
layout: default
title: Home
---

<p class="tagline">{{ site.description }}</p>

{% assign shown_posts = "" | split: "" %}
{% assign sorted_tags = site.tags | sort %}
{% for tag in sorted_tags %}
  <h2 class="tag-heading">{{ tag[0] | capitalize }}</h2>
  <ul class="post-list">
    {% for post in tag[1] %}
      {% unless shown_posts contains post.url %}
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
        {% assign shown_posts = shown_posts | push: post.url %}
      {% endunless %}
    {% endfor %}
  </ul>
{% endfor %}