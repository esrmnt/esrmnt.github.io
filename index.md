---
layout: default
title: Home
---

<p class="tagline">{{ site.description }}</p>

<hr class="dotted-separator" />

<div class="post-table">
  {% assign shown_posts = "" | split: "" %}
  {% assign sorted_tags = site.tags | sort %}
  {% for tag in sorted_tags %}
    {% for post in tag[1] %}
      {% unless shown_posts contains post.url %}
      <div class="post-row">
        <div class="post-date">{{ post.date | date: "%d %b, %Y" }}</div>
        <div class="post-title-wrap">
          <a class="post-title-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </div>
      </div>
      {% assign shown_posts = shown_posts | push: post.url %}
    {% endunless %}
    {% endfor %}
  {% endfor %}
</div>

<div class="tag-list">
  {% for tag in sorted_tags %}
    <span class="tag-label">#{{ tag[0] }}</span>
  {% endfor %}
</div>

<hr class="dotted-separator" />