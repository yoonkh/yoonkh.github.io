---
layout: default
title: Tags
parameter: tags
---

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}

{% assign tag_words = site_tags | split:',' | sort %}

{% for item in (0..site.tags.size) %}{% unless forloop.last %} {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
{{ this_word }} {{ site.tags[this_word].size }}
{% endunless %}{% endfor %}
