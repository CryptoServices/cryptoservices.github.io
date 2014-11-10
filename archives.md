---
layout: page
title: Archives
permalink: /archives/
---

<ul class="posts">
{% for post in site.posts %}
  <li><span class="hero">{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>