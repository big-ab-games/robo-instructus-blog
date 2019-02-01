---
preface: robo-2
title: World Scaling & Early Game Additions
excerpt_separator: <!--more-->
---
This week I've been finishing off the final game scaling logic and pondering the early game difficulty issues. Can I make this crucial first toe dip into programmatic puzzling a more pleasant one?

![](/assets/2019-02-01/top.jpg "This level is causing people to have hurty heads")

<!--more-->
## Early game design
The story of Robo Instructus' level design can be summarised as follows. I make a cool level. I don't think it's too hard. I get people to play it. They bounce off. So I try to figure out why, and generally it's requiring too much learning in too small an amount of time.

I've dealt with this by adding new levels requiring less knowledge to solve and themselves providing that knowledge at a more manageable pace. This can be seen by pointing out where the original first 3 levels now appear in the lineup.

At a very early point I remember having 3 pretty cool levels the 3rd being the first _proper_ puzzle. I quickly learnt that this required from players an insane ability to absorb knowledge in order to interact with properly. So I started adding levels in-between, trying to break up the concepts to be more approachable.

![](/assets/2019-02-01/orig-level-positions.jpg "Those original first levels, where are they now?")

So a couple of levels appear between 1 and 2, now maybe you have a chance understanding a loop, variables, unknown tiles, conditionals etc. Between 2 and 3 even more. In fact 3 is out of sight in the above picture because **seven** levels come between these levels now... I'm thinking of adding even more.

So how did I get it so wrong, does this level really require this much conceptual run up? Well not quite. When I added new levels I had to think of new simpler puzzles to spread the cognitive load. However, these new puzzles required their own new novel twists and complexity. Sometimes these new concepts needed yet more levels to help introduce them.

And here I am again with the first data-store level, currently level 5. It's introducing too much at once as I once again rush to get people into the _real game_ below. My answer is to yet again try to split out some of the concepts into another level.

There is a cost to all this of course, the early game could get bulked out too much and some players put off a game before they properly get into it. So I'm doing my best to avoid that, and indeed every single level offers a new challenge so should never be boring. The game is also grindless, if you know the solution just type it and click play - level done. No waiting about required.

This process is slow, because I tend to need playtesting feedback to spot difficulty spikes in the levels. That feedback has now come in for alpha-2.1, so expect changes. On the other hand I'm quite happy with the first 4 levels learning curve, so there is some good news!

## World scaling
Last week I signed off by noting that while the game's scaling was _all fancy and that_, scaling the actual game world wasn't in yet. This week I addressed that issue. Now the full game will scale gracefully for any reasonable resolution and aspect ratio.

![](/assets/2019-02-01/4ri.jpg "Different resolution sizes all equal in scaling")

## Next steps
February is going to be busy for me with lots of work on art integration, trailer creation and story writing. Lots of exciting improvements coming this month.

##### Comment on [twitter](https://twitter.com/bigabgames/status/1091378122958753793) | [facebook](https://www.facebook.com/bigabgames/posts/2278633525557355)
