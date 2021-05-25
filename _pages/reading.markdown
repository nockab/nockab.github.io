---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: default
title: Reading
permalink: /reading
---
## Book Log
<div class="post-grid">
  {% assign sorted = site.reading | sort: 'date_read' | reverse %}
  {% for book in sorted %}
  <div class="post-list-element">
    <date>{{ book.date_read | date: "%Y-%m-%d" }}</date>
    <p class="post-preview">{{ book.title | truncate: 57 }}</p>

    <!-- <small>{{ book.content }}</small> -->
  </div>
  {% endfor %}
</div>
