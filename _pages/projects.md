---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
---
This page lists various group and personal projects I've worked on outside of my main research.

{% include base_path %}

{% assign sorted_projects= site.projects | sort:"order" %}
{% for proj in sorted_projects %}
  {% include archive-single.html %}
{% endfor %}
