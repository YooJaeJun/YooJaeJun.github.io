---
permalink: /categories/GameDevelopment/
title: "Game Development"
layout: category
author_profile: true
sidebar_main: true
# taxonomy: 게임개발
---
{% assign posts = site.categories.GameDevelopment %}
{% for post in posts %} 
{% include archive-single.html type=page.entries_layout %} 
{% endfor %}