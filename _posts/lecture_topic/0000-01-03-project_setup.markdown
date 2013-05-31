---
layout: lecture_topic
title: Django Project Setup and Config
categories : 'lecture_topics'
permalink : /lecture-topics/setup_and_config
exercise_id : /exercises/setup_and_config
lecture_id : /lectures/setup_and_config
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


