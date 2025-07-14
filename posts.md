---
layout: default
title: "All Posts"
permalink: /posts/
---

# All Posts

{% for post in site.posts %}
## [{{ post.title }}]({{ post.url }})
*{{ post.date | date: "%B %d, %Y" }}*

{{ post.description }}

**Categories:** {{ post.categories | join: ", " }}  
**Tags:** {{ post.tags | join: ", " }}

---
{% endfor %}