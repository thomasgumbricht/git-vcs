---
layout: page
title: git version control system
excerpt: "An archive of articles sorted by date."
search_omit: true
---

Hands-on instructions for how to setup and get started with git version control system. Detailed commands and syntax are written from Mac OSX.

<ul class="post-list">
{% for post in site.categories.git %}
  <li><article><a href="{{ site.url }}{{ post.url }}">{{ post.title }} <span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %d, %Y" }}</time></span>{% if post.excerpt %} <span class="excerpt">{{ post.excerpt | remove: '\[ ... \]' | remove: '\( ... \)' | markdownify | strip_html | strip_newlines | escape_once }}</span>{% endif %}</a></article></li>
{% endfor %}
</ul>
