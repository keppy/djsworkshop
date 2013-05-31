---
layout: topic
title: Django Urls and Views
categories : [ 'topics', 'exercises', 'lectures' ]
permalink : /topics/urls_and_views
exercise_id : /exercises/urls_and_views
lecture_id : /lectures/urls_and_views
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


