---
preface: robo-2
excerpt_separator: <!--more-->
---
[Yesterblog I got excited](/2018/08/17/painting-the-stack-upon-the-world.html) about my new ability to store data information along with the actual stack values of the game's solutions. This allows the game to figure out that some number on the stack is, for example, a location id. This means I can do cool new stuff like rendering which locations you have saved in your stack. This week I have a more practical application than painting triangles different colours, and with it a new alpha release.

![](/assets/2018-08-24/top.jpg "Boom; Stack locations")

<!--more-->

The theme of this week turned out to be data visibility. My work on exposing stack locations made me think more about improving & extending the information the game can show you.

## Stack locations
The first and biggest improvement is showing that location data on the world. Highlighting the variable name itself on the tile shows you exactly where a given location is, or all the locations in an array. A good sign after developing something like this, is that it seems a vital feature now. This massively increases the visibility of just what is going on in later puzzles.

I couldn't quite figure out how to make it look _good_ though. But found shoving the name in the middle of the tile, with a colour code made it quite helpful ... if not pretty. Still cool though, ugly cool is still cool.

<video src="/assets/2018-08-24/stack-locations.mp4" controls></video>

If you're confused about where the names come from, they're literally the variable names I used in the solution code. So ***ok_tiles[]*** is the sequence I store all the ids I think are safe to move onto, ***front_loc*** is the tile I'm investigating. You can actually see ***item*** and ***el*** flashing around sometimes, they come from my ***contains*** function.

```kotlin
fun contains(list[], item)
    for el in list[]
        if el is item
            return 1
```
When was the last time you _actually saw_ iteration? That's got to worth the price of admission right? ...Well maybe not everyone gets excited about these things, but if you do you are already the target audience of Robo Instructus.

## Live score statistics
Stack locations aren't the only thing I've been hitting out the park. How about some live stats as your solution is running. This lets you see how they go up as the code runs, or steps forward while paused. This way players can work out what these values mean implicitly without me ever explaining them!

![](https://user-images.githubusercontent.com/2331607/44598378-b6636600-a7ca-11e8-8fa1-6819f071d3d2.gif "This makes perfect sense. Everyone understands these. Shut up")

Ok maybe you're right I should still explain them somewhere...

## Inline debugger improvements
Augmenting the existing inline debugging of stack values I added showing the value of the last function call, in case you didn't bother saving it on the stack.

![](https://user-images.githubusercontent.com/2331607/44598502-1eb24780-a7cb-11e8-80c5-65335f485c04.png "More inline burgundies!")

That example above didn't show anything before, because the solution funnels the ***robo_scan()*** result straight into a comparison. The value never has time to just sit on the stack and _exist_. Showing it should be a nice improvement, and particularly for new & early game players.

I've also used the stack data storage mechanism for a smaller job, if I can store than a value is a location I can also store that the value is something else. So I used this to show inline what direction a direction code means.

![](https://user-images.githubusercontent.com/2331607/44598683-b9128b00-a7cb-11e8-9991-c24db1cdfd47.png "It's up")

## Alpha 1.18
These new features are available for my slumbering alpha testers in the form of alpha-1.18. Man when I slap some sexy art on this game I'm getting some new cool testers and you'll be sorry you never liked me when I was ugly.

I mean the game. Constructive feedback for the game.
