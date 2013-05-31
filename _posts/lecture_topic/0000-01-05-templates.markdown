---
layout: lecture_topic
title: Django Templates
categories : 'lecture_topics'
permalink : /lecture-topics/templates
exercise_id : /exercises/templates
lecture_id : /lectures/templates
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


