---
title: "싸피"
layout: archive
permalink: categories/ssafy
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Ssafy %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}