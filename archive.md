---
layout: default
title: Blog List
---

<h2>BLOG LIST<\h2>
{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
