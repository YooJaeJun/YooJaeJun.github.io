---
permalink: /categories/
title: "Category"
layout: category
author_profile: true
sidebar_main: true
---
<div class="page clearfix">
  <div class="left">
    <h1>{{page.title}}</h1>
    <hr>
    <ul>
      {% for category in site.categories %}
      <h2 id="{{category | first}}">{{category | first}}</h2>
      {% for posts in category %}
      {% for post in posts %}
      {% if post.url %}
      <li>
        <time>
          {{ post.date | date:"%F" }} {{ post.date | date: "%a" }}.
        </time>
        <a class="title" href="{{ post.url | prepend: site.url }}">{{ post.title }}</a>
      </li>
      {% endif %}
      {% endfor %}
      {% endfor %}
      {% endfor %}
    </ul>
  </div>
</div>