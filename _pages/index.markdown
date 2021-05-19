---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: default
title: Home
permalink: /
---

<div class="post-grid">
  {% for post in site.posts %}
  <div class="post-preview-block">

  <h4><a href="{{ post.url }}" class="post-preview">{{ post.title }}</a></h4>
  <p>{{ post.date | date: "%b %-d, %Y" }}</p>
  </div>
  {% endfor %}
</div>
