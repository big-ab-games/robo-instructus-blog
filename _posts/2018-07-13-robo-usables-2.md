---
preface: robo-2
title: More Robo Usables & Alpha-1.14
---
Following from [last weeks look at usable tiles](/2018/07/06/robo-usables.html) this week lets take a look at another "data point", as I'm currently calling these, players will need to tackle on the road to robo mastery. The **direction data point**.

<p align="center">
  <img align="center" src="/assets/2018-07-13/usable-dir.png" title="Follow the arrow!" />
</p>

***"Direction data points contain directions relative to that tile."*** The game will tell you. These tiles will return a direction when you ***robo_use()*** them. ***1*** means up, ***2*** means right etc, of course everything is an integer in Robo Instructus.

If we take a look at the first level you encounter these hopefully you'll see how they can be helpful.

<p align="center">
  <img align="center" src="/assets/2018-07-13/direction-level.png" title="The very first direction level" />
</p>

Similarly to the last weeks levels, these don't have visible (ie ***robo_scan()***-able) exits. This is where the directions come in, they point to safe unknown tiles. In these simpler levels that unknown tile turns out to be the exit.

So it starts simple as always, but this brings a new concept for the players that was previously only encountered later in the launcher tile mid-game. That concept is keeping track of the robots orientation. Because the directions contained in these tiles are absolute, north/south/east/west, you need to be aware of which way you're actually facing to make sense of them.

It's actually pretty doable to do this once you have a go. So I think this should prove a pretty satisfying challenge that isn't explicitly set by the game.

### Alpha 1.14
Since data points are not just late game content they've appeared in the latest alpha released today. ***alpha-1.14*** features **6 new levels** to conquer. This could be a great time for my sleepy alpha testing group to wake up and play the game again! You guys are still there right? I'm considering recruiting some more peeps to help test the game, but also want to hold off for the final art. Hmmm...

### Other News
The other thing I've been working on this week is late game levels you tackle with robot & probe. [Read about the probe](/2018/06/22/probo-instructus-p2.html) if you missed that. These levels are quite exciting and really open up possibilities compared to the single-robot early & mid game. I'll talk a little more about the cool late game challenges in the coming weeks.
