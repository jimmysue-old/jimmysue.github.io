---
    layout: default
    title: Post by Category
    permalink: /categoryview/
    sitemap: false
---


<header id="post-header">
    <h1 id="post-subtitle">Articles By Category {{ page.categories }}</h1>
</header>
<hr>
{% assign tags = site.categories | sort %}
{% assign sorted_posts = site.posts | sort: 'title' %}
<div> 
{% for tag in tags %}
<a href="#{{ tag | first | slugify }}">{{ tag | first | replace: '-', ' ' }}({{ tag | last | size }})</a>{% if forloop.last == false %} &nbsp; {% endif %}{% endfor %}
</div>
<hr>

{% for tag in tags %}

<h3 class="archivetitle">{{ tag | first | replace:'-', ' ' }} <i class="badge">{{ tag | last | size }}</i> </h3>

<ul>{% for post in sorted_posts %}{%if post.categories contains tag[0]%}<li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a> 
{% if post.author %} &raquo; <span class='author'>{{ post.author }}</span>{% endif %}{% if post.date %} &raquo; <span class='time'>{{ post.date | date_to_string }}</span>{% endif %}</li>{%endif%}{% endfor %}</ul>
{% endfor %}