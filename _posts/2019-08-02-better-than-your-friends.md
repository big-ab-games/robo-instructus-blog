---
preface: robo-2
title: Compare Against Your Friends
excerpt_separator: <!--more-->
---
Hot on the heels of last week's score visualisation improvements, today brings Robo Instructus **1.3**. The big new feature is one I've been planning to have for a long time now, comparing your best scores against your friends.

![](/assets/2019-08-02/top.jpg "Wtf! I made the game ffs!")
<!--more-->

This feature is a close one to my heart. _Being better than most of the world?_ Nah I'm ok thanks, sounds hard. _Being better than your mates?_ Let's do it!

![](https://user-images.githubusercontent.com/2331607/62379292-92fa7c80-b53e-11e9-8a79-4bd486edf725.jpg "Solution size is the true score really, honestly I can't really remember why I included the others now that I think about it. There's probably a bug too maybe. Plus I wasn't really trying anyway. These things don't bother me at all, I'm totally laid back about these things.")

Or maybe not.

Right now this is limited to Steam users, as I'm not sure there's anything similar to the friend system over on Itch. Though it is implemented in a general purpose way that could work with other stores in future.

## Global best score capping
The game's score graphs are generally doing their job well, particularly now outliers are filtered out. However, there is another area where I wasn't satisfied with how they were being interpreted. When I published 1.1 I explained how the score bars work with this image.

![](/assets/2019-08-02/1.1-graph.jpg "Scores ala 1.1 explained")

This image explains that the score summaries group scores into ranges, or buckets, of scores to show approximately where most other players are. The it's possible no player got the bottom of the range.

However, new players are still taking a look at these graphs and reading that their early solutions aren't optimal when in some ways they might be. This really isn't ideal so I set to thinking of simple ways to improve the clarity, particularly in the early levels.

I settled on tracking the global lowest score anyone has achieved and including this in the score summary. The graphs can then cap the left most bar to that global lowest score. This makes the graphs less uniform and could result in very thin left bars in some cases. However, it does add value now the graphs show the best score that anyone has got on all levels.

![](/assets/2019-08-02/capped.jpg "Yep, you can solve this level with a solution size of 4 phrases. The other two are perfect though so chin up!")

In the early levels it'll much more clearly show you that yes your solution actually was optimal and it's nice to see just how low people can get the scores even when yours isn't the lowest (this is most of the time for me).

##### Comment on [twitter](https://twitter.com/bigabgames/status/1157330395320541184) | [facebook](https://www.facebook.com/bigabgames/posts/2587119501375421)
