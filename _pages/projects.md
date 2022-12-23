---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
---
This page lists various group and personal projects I've worked on outside of my main research.

{% include base_path %}

{% for post in site.projects reversed %}
  {% include archive-single.html %}
{% endfor %}
