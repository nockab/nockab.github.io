---
layout: default
title: Home
permalink: /
---

<ul class="post-list">
  {% for post in site.posts %}
    <li class="post-item">
      {% if post.image %}
        <img src="{{ post.image }}" alt="" class="post-image">
      {% endif %}
      <div class="post-content">
        <div class="post-header">
          <a href="{{ post.url }}" class="post-link">{{ post.title }}</a>
          <div class="post-date">{{ post.date | date: "%Y.%m.%d" }}</div>
        </div>
        {% if post.excerpt %}
          <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
        {% endif %}
      </div>
    </li>
  {% endfor %}
</ul>
