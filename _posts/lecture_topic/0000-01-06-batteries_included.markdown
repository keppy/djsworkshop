---
layout: lecture_topic
title: Django Batteries Included
categories : 'lecture_topics'
permalink : /lecture-topics/batteries_included
exercise_id : /exercises/batteries_included
lecture_id : /lectures/batteries_included
---

__Lecture__
{% for lect in site.categories.lectures %}
{% if lect.id == page.lecture_id %}
[{{lect.title}}]({{lect.url}})
{% endif %} 

{% endfor %}

   __Exercise__
{% for exer in site.categories.exercises %}
{% if exer.id == page.exercise_id %}
[{{exer.title}}]({{ exer.url }})
{% endif %} 
{% endfor %}


