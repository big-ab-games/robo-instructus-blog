---
preface: robo-2
title: Puzzle Design Complete, New Debugging Tools & Alpha-1.15
---
This week Robo Instructus has reached an important milestone: All primary level design is now complete! Over 30 individual levels to conquer through code. But that's not all folks, how about improved debugging tools and a brand new alpha-1 release?

![](/assets/2018-07-20/late-level.png "It gets harder, but you get a juicy probe")

## The puzzles are done
The game consists of 3 "arcs" of levels. Each arc introduces a new major concept and ramps up the difficulty in dealing with that concept. The climax of each arc is an optional "challenge" level that will be a bit of a pain and require all the learning from previous levels plus a little extra. The current alpha-1.x builds are the 1st arc of levels, it's the largest arc as it has to teach players the most by far. The concept of the first arc is pretty much _"programming"_ after all.

I said the "primary level design" is complete because I may add more levels to compliment what's already there. However, each arc now feels complete and the game-length & pacing seem good. Of course, play-testing will tell me how true that really is.

I actually have a lot of ideas that I haven't used in any of the 3 arcs yet. In the end I wanted to make the game a tight enjoyable experience, without too many new things getting the way of the core gameplay. After release I'll find out if the game finds it's audience and can think about expansion.


## New debugging tools
The current debugging tools consist of being able to pause any running solution at any time. When paused you can investigate the current state at your leisure, and you can click "next" to progress by a single expression.

<p align="center">
  <img align="center" src="/assets/2018-07-20/debug-next.png" title="Next!"/>
</p>

This allows you very fine grained ability to "step forward" through a solution and find out what isn't working correctly. However, in more complex solutions this can turn out to be a little _too_ fine grained. It can get stuck in loops and take you into bits of the code that you're not particularly interested in debugging.

So I've added a new debug step "step down" that unpauses the code until the execution moves _down_ to a later line, or if it exits a function call.

<p align="center">
  <img align="center" src="/assets/2018-07-20/debug-down.png" title="Down!"/>
</p>

With this you can _ctrl-click_ or press down to skip past a function call, or skip out of a loop.

Another addition this week is the ability to debug either the robot _or_ the probe as you please. Let's see both _(you don't have to keep moving the cursor away from the button like I did, I just did that to demonstrate single clicks)_.

<video src="/assets/2018-07-20/debugging.mp4" controls></video>

Come to think of it, it might be a bit of a weird concept, though it does work. "Step down" is kind of a mix of the standard "step over" and "step out of". I may replace this functionality in future by adding both of those instead. To be honest I don't debug often so perhaps this isn't as obvious to me as it should be. I've never debugged the Robo Instructus game code. Still that's written in rust so compilation is more than half the battle there.

## Alpha-1.15
Since "step down" may help people in alpha-1.x and also since I've made a few other fixes here and there, I making yet another alpha-1 release. With the now larger length of the first arc I managed to fit in the final tutorials that I couldn't seem to cram in anywhere. Now all features of the language and game are at least _somewhat_ explained in the first arc.

![](/assets/2018-07-20/boolean-operators.jpg "Explaining stuff is probably for the best")

Boolean operators were a bit of a weird one to fit in strangely. They seem so fundamental _(so should be explained asap)_, yet actually never prove _necessary_ to use. As such they'll explained fairly late into arc-1. But hopefully the examples here show real usages that could be useful.

## Learning stuff
Talking about the tutorials, I still feel this is the area I need to improve the most. But I also need the most help from my testers. Where did you hit a brick wall, what didn't make sense or could be better? While I'm trying to avoid verbosity, I'm not _intentionally_ trying to be obtuse with these tutorials. So let me know how to improve them test peeps!

##### Comment on [reddit](https://www.reddit.com/r/rust_gamedev/comments/90gwct/robo_instructus_puzzle_design_is_now_complete/) | [twitter](https://twitter.com/bigabgames/status/1020325591701180417) | [facebook](https://www.facebook.com/bigabgames/posts/1979184088835635)
