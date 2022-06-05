---
permalink: /categories/Language/
title: "Language"
layout: category
author_profile: true
sidebar_main: true
# taxonomy: 언어 지식
---
{% assign posts = site.categories.Language %}
{% for post in posts %} 
{% include archive-single.html type=page.entries_layout %} 
{% endfor %}