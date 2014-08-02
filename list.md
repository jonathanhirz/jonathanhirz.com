---
layout: otherPage
title: Archive
---
If you prefer to browse categorically, <a href="/archive/">click here</a>.

<ul>
  {% for post in site.posts %}

    {% unless post.next %}
      <h3>{{ post.date | date: '%Y' }}</h3>
    {% else %}
      {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
      {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
      {% if year != nyear %}
        <h3>{{ post.date | date: '%Y' }}</h3>
      {% endif %}
    {% endunless %}

    <li>{{ post.date | date:"%-d %b" }} <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>