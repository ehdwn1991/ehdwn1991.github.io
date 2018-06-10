---
layout: page
title: Concept of Embeded and Deep learning
description: >
  임베디드 딥러닝 개론 스터디

slug: study_intro_coe
---



{% for post in site.study %}
{% if post.study contains page.slug and post.title != "sample"%}
   <a href="{{ post.url }}">
       {{ post.title }} </a>
{% endif%}
{% endfor %}

