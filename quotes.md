---
layout: page
title: Quotes
---

<blockquote class="green">
Sometimes it's the very people who no one imagines anything of who do the things no one can imagine.
- Alan Turing, The Imitation Game.
</blockquote>

{% for tag in site.tags %}
  <h3>{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}