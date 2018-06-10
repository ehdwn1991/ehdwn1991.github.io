---
layout: page
title: Progaming Language study of C
description: >
  C언어 스터디

slug: study_lang_c
---

  <header>
    <h1 class="page-title">{{ page.title }}</h1>
    {% include message.html text=page.description hide=page.hide_description %}
  </header>
  <hr class="sr-only"/>
{% endif %}

{{ content }}


{% for post in site.study %}
{% if post.study contains page.slug%}
   <a href="{{ post.url }}">
       {{ post.title }} </a>
{% endif%}
{% endfor %}
