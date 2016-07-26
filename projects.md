---
title: Projects
layout: page
---

## Papers

<ul>
{% for post in site.categories.papers %}
<li>
<a href="{{post.url}}">
{{ post.title }}
</a>
</li>
{% endfor %}
</ul>

## Other projects

<ul>
{% for post in site.categories.projects %}
<li>{{ post.title }}</li>
{% endfor %}
</ul>
