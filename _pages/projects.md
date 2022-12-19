---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
---
This page lists various group and personal projects I've worked on.

{% include base_path %}

{% for post in site.projects reversed %}
  {% include archive-single.html %}
{% endfor %}
