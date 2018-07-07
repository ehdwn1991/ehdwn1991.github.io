---
layout: post
title: Study Embeded lecture Collection Post Sample
comments: true
description: >
  

study: [study_embeded]
categories: [personal_prob]
tags: [c,backjoon_level]
date: 2018-05-05
author: author2
---




  {% assign posts = site.posts%}
  {% assign s_study = site.study | where:"layout","post"%}
  {% assign posts = posts | concat: s_study %}
  {% for post in posts %}
    <url>
      <loc>{{ site.url }}{{ post.url }}</loc>
      {% if post.lastmod == null %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
      {% else %}
        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>
      {% endif %}

      {% if post.sitemap.changefreq == null %}
        <changefreq>weekly</changefreq>
      {% else %}
        <changefreq>{{ post.sitemap.changefreq }}</changefreq>
      {% endif %}

      {% if post.sitemap.priority == null %}
          <priority>0.5</priority>
      {% else %}
        <priority>{{ post.sitemap.priority }}</priority>
      {% endif %}

    </url>
  {% endfor %}