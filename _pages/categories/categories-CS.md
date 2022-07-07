---
permalink: /categories/CS/
title: "CS"
layout: category
author_profile: true
sidebar_main: true
# taxonomy: 컴퓨터 공학 지식
---
{% assign posts = site.categories.CS %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}