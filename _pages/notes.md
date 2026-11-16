---
layout: page
permalink: /notes/
title: course notes
description: Course notes and mathematical writing by Hongyu Zhu.
nav: true
nav_order: 1
---

These are personal working notes. They may contain errors; corrections and suggestions are welcome by email.

## Available

{% assign available_notes = site.data.course_notes | where: "status", "available" %}
{% for note in available_notes %}

<h3>{{ note.title }}</h3>
<p>{{ note.description }}</p>
<ul>
{% for file in note.files %}
  <li><a href="{{ file.path | relative_url }}">{{ file.label }}</a></li>
{% endfor %}
</ul>
{% endfor %}

## Forthcoming

{% assign forthcoming_notes = site.data.course_notes | where: "status", "forthcoming" %}

<ul>
{% for note in forthcoming_notes %}
  <li>{{ note.title }} — <em>coming soon</em></li>
{% endfor %}
</ul>
