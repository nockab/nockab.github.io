---
layout: default
title: Blog
permalink: /blog
---

## My Blog Posts not
<div class="post-grid">
  {% for post in site.posts %}
  <div class="post-preview-block">

  <h4><a href="{{ post.url }}" class="post-preview">{{ post.title }}</a></h4>
  <p>{{ post.date | date: "%b %-d, %Y" }}</p>
  </div>
  {% endfor %}
</div>
