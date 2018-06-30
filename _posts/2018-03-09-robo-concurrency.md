---
preface: robo-2
---
I'm now working on the final arc of levels for Robo Instructus. Let's take a look at one of the new concepts players will have to struggle with as they close into the game's closing puzzles. The concept is _concurrency_.

![](/assets/2018-03-09/rick.jpg "Do two things at once like Rick. Cape optional.")

It isn't a dodgy kind of money, it's when more than one thing happens at once. That means coding logic that will run at the same time, perhaps communicating or interfering with each other.

More precisely you'll be able to code another robotic avatar and by only by using both unique robotic abilities will the levels be surpassable.

Concurrency in the real world can be tricky. Sometimes tricky-fun, but other times tricky-horrible. Horrible because they sometimes undermine entire programming concepts a programmer may have come to rely on. Well in short I'll be providing a slightly less scary version of concurrency in Robo Instructus, all within the behaviour of the existing language.

### Implementation concerns
My plans are all very well and good, but I'm still in progress actually implementing concurrent execution in-game. One issue is that all solutions must execute deterministically. This is definitely not a given with concurrent threads. I'm working on a game world synchronisation mechanism to save the day. Let's see how that works out!

### Other progress
I've also done a little optimization work this week as I noticed the game was starting to creep up in CPU usage at idle. I've also some fixes to the graph rendering, but no release this week. I'll save up the smaller changes for another _alpha-1.x_ release sometime later.

Once the final levels are designed and working I can finally get the final art done. Replacing the tile & robot artwork unlocks being able to promote the game much more. Trailer, launch site, widening the alpha-testing group much more to polish the experience. I'm really looking forward to hitting the next stage & seeing Robo Instructus in it's new skin!

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/839401/robo_instructus_robo_concurrency/) | [twitter](https://twitter.com/bigabgames/status/972182985452785665) | [facebook](https://www.facebook.com/bigabgames/posts/1806723232748389)
