---
layout: default
permalink: /guides/index.html
---

The list of guides:


{% for g in site.guides %}
* [{{g.title}}]({{ g.url | prepend: site.baseurl }})

{% endfor %}     
