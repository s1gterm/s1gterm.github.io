---
permalink: /
layout: splash
author_profile: false
read_time: false
show_date: true
entries_layout: grid
classes: wide
title: "Posts" 
header:
  overlay_image: /assets/images/home.jpg
  overlay_color: "#000"
  overlay_filter: "0.5"
---

{% if paginator %}
  {% assign posts = paginator.posts %}
{% else %}
  {% assign posts = site.posts %}
{% endif %}

{% for post in posts limit:1 %}
  {% if forloop.index == 1 %}
    {% include post_hero type="left" wrapper="both" title=post.title excerpt=post.excerpt overlay_image=post.header.overlay_image overlay_color="#000" overlay_filter="0.5" btn_label="Read More" btn_class="btn--primary btn--small" url=post.url %}
  {% endif %}
{% endfor %}

{% for post in posts offset:1 %}
    {% assign mod_index = forloop.index | modulo: 3 %}
    {% if mod_index == 1 and forloop.last %}
      {% assign wrapper = 'both' %}
    {% elsif mod_index == 1 %}
      {% assign wrapper = 'start' %}
    {% elsif mod_index == 0 or forloop.last %}
      {% assign wrapper = 'end' %}
    {% else %}
      {% assign wrapper = '' %}
    {% endif %}
    {% include post_row wrapper=wrapper title=post.title image_caption=post.title excerpt=post.excerpt image_path=post.header.teaser btn_label="Read More" btn_class="btn--inverse btn--small" url=post.url %}
    
{% endfor %}

{% include paginator.html %}