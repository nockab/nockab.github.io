---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: default
title: Home
permalink: /
---
## Notes on Life and Personal Productivity
<div class="post-grid">
  {% for post in site.posts %}
  {% if post.public == True %}
  <div class="post-list-element">
    <a href="{{ post.url }}" class="post-preview">{{ post.title }}</a>
    <date>{{ post.date | date: "%Y-%m-%d" }}</date>
  </div>
  {% endif %}
  {% endfor %}
</div>
