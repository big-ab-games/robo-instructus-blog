---
# enable liquid template
preface: false
big_logo: true
---
Big AB Games are developing programming puzzle game [Robo Instructus](https://www.roboinstruct.us) released July 16th 2019, read about it below.

{% for post in site.posts limit:1 %}
##### Posted on {{post.date | date: "%A %e-%b-%Y"}}

> ## {{ post.title }}
> {{ post.excerpt }}
[<b>Read the rest of this post</b>]({{ post.url }})


{% endfor %}
