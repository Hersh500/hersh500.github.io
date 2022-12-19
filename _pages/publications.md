---
layout: archive
title: "Publications and Writing"
permalink: /publications/
author_profile: true
---
{% include base_path %}
## Publications
{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}

## Technical Writing and Blog Posts
{% for post in site.writing reversed %}
  {% include archive-single.html %}
{% endfor %}
