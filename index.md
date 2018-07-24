---
# enable liquid template
preface: false
big_logo: true
---
Big AB Games are developing robot engineering puzzle game **Robo Instructus**, read about it below.

{% for post in site.posts limit:1 %}
##### Posted on {{post.date | date: "%A %e-%b-%Y"}}

> ## {{ post.title }}
> {{ post.excerpt }}
[Read the rest of this entry]({{ post.url }})


{% endfor %}
