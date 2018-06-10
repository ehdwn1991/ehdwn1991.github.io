---
layout: page
title: Study
description: >
  
menu: true
order: 2
---


<!-- study컬렉션에 있는 모든 포스트와 페이지등 모든 문서 보여줌 현재 페이지 뺴고 -->
<!-- {% for test in site.study %}
{% if test.title != page.title%}
<a href="{{ test.url | prepend: site.baseurl }}">
       {{ test.title }}
   </a>
<time class="heading faded fine" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date:format }}</time>
<p class="post-excerpt">{{ test.description | truncate: 160 }}</p>
{% endif%}
{% endfor %}     -->


<!-- ## ttt
{% assign date_formats  = site.data.strings.date_formats               %}
{% assign list_group_by = date_formats.list_group_by | default:"%Y"    %}
{% assign list_entry    = date_formats.list_entry    | default:"%d %b" %}
{%for asd in site.study %}
{% if asd.tags contains "c"%}
{{asd.title}}
  <time class="heading faded fine" datetime="{{ post.date | date_to_xmlschema }}">{{ asd.date |date:list_entry }}</time>
{% endif%}
{% endfor%}
## aaaa -->

<!-- {% assign posts = site.study | where:'tags',"c" %}
{% assign tt = site.tags["c"] | sort: 'title','first' | reverse%}
{% assign posts = posts | concat: tt%}
{% for post in posts%}
{{post.title}}
{% endfor%} -->

<!-- study콜렉션에 있는 layout이 page인 문서들을 보여줌-->
{% for test in site.study %}
{% if test.title != page.title %}
    {% if test.layout == "page" %}
    {% assign studycoll = test.title | join:'|' | append:'|' %}
    {% assign scoll = scoll | append:studycoll %}

<h2><li><a href="{{ test.url | prepend: site.baseurl }}">
       {{ test.title }} </a></li></h2>

    {% endif %}
{% endif%}
{% endfor %}  
