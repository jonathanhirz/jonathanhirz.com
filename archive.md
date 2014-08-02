---
layout: otherPage
title: Archive
---
If you prefer to browse chronologically, <a href="/list/">click here</a>.

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