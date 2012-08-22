---
layout: default
title: froschi.github.com
---
# Welcome to froschi.github.com

You have found a wobsite. You rascal.

## Updates

{% for post in site.categories.update %}
* {{ post.date | date: "%F" }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
