---
layout: page
---

<h2>Media related to {{ page.eventname }}</h2>

{{ content }}


{% if page.talks_files %}
<h3>Talks</h3>

<ul>
{% for mfile in page.talks_files %}
<li><a href="{{mfile}}">{{mfile}}</a></li>
{% endfor %}
</ul>

{% endif %}

{% if page.other_files %}
<h3>Other media</h3>

<ul>
{% for mfile in page.other_files %}
<li><a href="{{mfile}}">{{mfile}}</a></li>
{% endfor %}
</ul>

{% endif %}
