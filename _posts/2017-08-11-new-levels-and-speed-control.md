---
preface: robo
---

The rusty road winds ever onward to my goal of a playable alpha build. I need a nice alpha *MVP* to gather feedback for this strange and wonderful game of robot engineering. This week I finished designing the alpha challenge levels and the level APIs (the tools you'll use to complete the levels). We now have selectable world speed (how fast the robot moves about) and selectable code execution speed UIs.

### New levels
First lets take a peek at the new levels. I started to have real actual in-game fun solving these myself. The last level is actually quite hard, maybe too hard... but I thought it'd be nice to have a remaining challenge even in the alpha. *I've hidden my code solutions in all the videos to avoid spoiling the experience*.

<video src="/assets/2017-08-11/new-levels.mp4" controls autoplay loop></video>

These should be enough to challenge all my lovely alpha testers. They may be a little tougher than they initially appear, remember the grey tiles *could* be a tile, or not.

### Speed control
You may notice in the top corners of the both areas a new UI control. This allows control of code execution speed  world run speed.

![](/assets/2017-08-11/speed-switch.gif)

The code execution speed allows slowing down how the code runs so you can see & understand what's going on. When running slowly you can see the current expressions highlighting and moving around depending on your logic. This isn't something programmers generally get when learning a language, so it's somewhat novel and I hope it'll be a useful tool in understanding how to speak with this game. When running the code at the fastest speed, it's pretty much going to be instant and just be pausing whenever it needs the robot to actually move or do something.

In the top right corner we have a similar UI for controlling world speed. This reduces/increases the time it takes for our robot to follow commands.

<video src="/assets/2017-08-11/selectable-speed.mp4" controls></video>

With the code execution speed you can also pause it altogether, can progress an expression at a time.

As you can imagine if you select max code execution speed *and* max world speed the game is really going to zip by. While its hard to see whats happening like this, this is a useful setting for large levels you may have already completed, but would like to optimise or play around with.

Let's see how fast it can go on a more complex level!

<video src="/assets/2017-08-11/max-speed.mp4" controls></video>

I had originally de-scoped speed control for the alpha, but as I was testing the later levels it quickly become desirable to avoid waiting for the robot to traverse larger sections. On the other hand at the beginning it's natural to want it to move more slowly as you test your initial algorithms.

After finishing the UI logic & adding world speed selection, it wasn't too difficult to add a code execution speed UI too.

All in all some decent progress towards the first Robo Instructus alpha. The remaining items are improved animations for the now finished APIs, tutorials, level completion dialogs, code wrapping/scrolling/rendering improvements & in-game error highlighting/hinting.

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/6t15sn/robo_instructus_the_game_where_you_actually_need/) | [twitter](https://twitter.com/alexbutlergames/status/895999901066301440) | [facebook](https://www.facebook.com/alexbutlergames/posts/1539190676168314)
