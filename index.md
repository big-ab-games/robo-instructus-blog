---
# enable liquid template
preface: false
big_logo: true
---
I'm Alex Butler, in April 2017 I quit my job to start making my own games. I post gamedev progress & ideas here.
<br/>I'm also on [twitter](https://twitter.com/alexbutlergames) & [facebook](https://www.facebook.com/alexbutlergames).
For my other code stuff see [github](https://github.com/alexheretic).


{% for post in site.posts limit:1 %}
##### Posted on {{post.date | date: "%A %e-%b-%Y"}}

> ## {{ post.title }}
> {{ post.excerpt }}
[Read the rest of this entry]({{ post.url }})

{% endfor %}
