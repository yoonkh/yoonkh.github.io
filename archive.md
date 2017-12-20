---
layout: page
title: Archive
parameter: archive
---

{% for post in site.posts %} {% capture month %}{{ post.date | date: '%m%Y' }}{% endcapture %} {% capture nmonth %}{{ post.next.date | date: '%m%Y' }}{% endcapture %} {% if month != nmonth %} {% if forloop.index != 1 %}{% endif %}

{{ post.date | date: '%Y년 %m월' }}
{% endif %}
{{ post.title }} {{ post.date | date: "%Y-%m-%d" }}
{% endfor %}
