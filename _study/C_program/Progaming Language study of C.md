---
layout: page
title: Progaming Language study of C
description: >
  C언어 스터디

slug: study_lang_c
---



{% for post in site.study %}
{% if post.study contains page.slug%}
   <a href="{{ post.url }}">
       {{ post.title }} </a>
{% endif%}
{% endfor %}
