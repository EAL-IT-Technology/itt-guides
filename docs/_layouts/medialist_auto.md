---
layout: page
---

{% assign eventname =  page.url | split: "/" | last  %}
{% assign event = site.collections | where: "label", eventname | first %}
{% assign mediapath = "/media/" | append: eventname | append: "/" %}
{% assign path_other = mediapath | append: "Other" %}
{% assign path_talks = mediapath | append: "Talks" %}
{% assign have_talks = false %}
{% assign have_other = false %}

{% for static_file in site.static_files %}
  {% if static_file.path contains path_talks %}
    {% assign have_talks = true %}
  {% elsif static_file.path contains path_other %}
    {% assign have_other = true %}
  {% endif %}
{% endfor %}

<h2>Media related to {{ event.title }}</h2>

{{ content }}


<h3>Talks</h3>

{% if have_talks %}
{% assign path = mediapath | append: "Talks" %}

<ul>
{% for static_file in site.static_files %}
  {% if static_file.path contains path %}
  <li><a href="{{static_file.path}}">{{static_file.basename | append: static_file.extname }}</a></li>
  {% endif %}
{% endfor %}
</ul>
{% else %}
(no media from talks currently available)
{% endif %}

{% if have_other %}
<h3>Other media</h3>
{% assign path = mediapath | append: "Other" %}

<ul>
{% for static_file in site.static_files %}
  {% if static_file.path contains path %}
  <li><a href="{{static_file.path}}">{{static_file.basename | append: static_file.extname }}</a></li>
  {% endif %}
{% endfor %}
</ul>

{% endif %}
