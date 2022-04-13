---
title: "Handy Function"
layout: archive
permalink: tags/handy-function
---

{% assign posts = site.tags.handy-function %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}