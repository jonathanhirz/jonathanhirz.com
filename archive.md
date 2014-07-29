---
layout: otherPage
title: Archive
---

<ul>
{% for category in site.categories reversed %}
  <li>{{ category[0] }}
    <ul>
    {% for posts in category %}
      {% for post in posts %}
        {% if post.url %}
          <li><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date:"%-d %B %Y" }}</li>
        {% endif %}
      {% endfor %}
    {% endfor %}
    </ul>
  </li>
{% endfor %}
</ul>