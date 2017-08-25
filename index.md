---
# enable liquid template
preface: false
big_logo: true
---
I'm Alex Butler, in April 2017 I quit my job to start making my own games. I post gamedev progress & ideas here.

I'm developing robot engineering puzzle game **Robo Instructus**, read about it below.

<p align="center">
  <img align="center"
    src="/assets/main/robot.png"
    title="A 'Robo' to instruct ...us" />
</p>

{% for post in site.posts limit:1 %}
##### Posted on {{post.date | date: "%A %e-%b-%Y"}}

> ## {{ post.title }}
> {{ post.excerpt }}
[Read the rest of this entry]({{ post.url }})

{% endfor %}
