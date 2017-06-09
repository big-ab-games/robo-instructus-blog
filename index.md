---
# enable liquid template
---
I'm Alex Butler game designer and programmer. You've found yourself at my gamedev blog. For my other stuff see [github](https://github.com/alexheretic).


{% for post in site.posts limit:1 %}
##### Posted on {{post.date | date: "%A %e-%b-%Y"}}

> ## {{ post.title }}
> {{ post.excerpt }}
[Read the rest of this entry]({{ post.url }})

{% endfor %}
