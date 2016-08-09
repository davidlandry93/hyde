---
title: Posts
layout: page
---

{% for post in site.posts %}
<h2 class="post-title"><a href="">{{ post.title }}</a></h2>
<span class="post-date">{{post.date | date: '%Y-%m-%d'}}</span>

<blockquote>
{{ post.excerpt }}
</blockquote>
{% endfor %}
