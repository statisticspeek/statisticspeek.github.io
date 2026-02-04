---
layout: home
title: Informes
---

# Statistics Peek

Pequeños informes estadísticos.

## Informes recientes

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date: "%d/%m/%Y" }}
{% endfor %}
