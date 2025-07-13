---
layout: default
title: "Manikandaraj Srinivasan"
---

### Hi, I'm Mani

Software Engineer at heart, building scalable solutions and leading tech innovations as a Technical Manager.

- 🚀 Architecting cloud-native systems and microservices  
- 💡 Exploring AI, Algorithms, and AWS while writing insightful tech blogs  
- 🔧 Experimenting with Raspberry Pi projects and securing home networks  
- ⚙️ Enhancing CI/CD pipelines and automation strategies for efficient deployments

## Recent Blog Posts

{% for post in site.posts limit:5 %}
- [{{ post.title }}]({{ post.url }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

[View all posts →](/posts/)
