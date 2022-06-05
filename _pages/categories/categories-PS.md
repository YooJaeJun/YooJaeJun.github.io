---
permalink: /categories/PS/
title: "PS"
layout: category
author_profile: true
sidebar_main: true
# taxonomy: 코딩 테스트용 PS
---
{% assign posts = site.categories.PS %}
{% for post in posts %} 
{% include archive-single.html type=page.entries_layout %} 
{% endfor %}