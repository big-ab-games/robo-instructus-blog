---
preface: robo-2
excerpt_separator: <!--more-->
---
Back in November I introduced [a window to the stack](/2017/11/03/a-window-to-the-stack.html) with live inline debugging for Robo Instructus, and there was much rejoicing. This decorated your code with the current value of variables & contents of sequences. Very useful, but an area it didn't help as much with was location identifiers. These 4-digit codes uniquely identify a particular tile in the level and are something players have to grapple with more and more as they progress through the game. As they're confusing in isolation I spent a little time experimenting with how they could be better visualised.

![](/assets/2018-08-17/top.jpg "First contact with the location id")

<!--more-->

Location IDs are simple enough. Each tile gets a distinct number as it's id. The robot can read this id before stepping on it, and can get interesting locations (in id form) from other sources. So perhaps a data point contains the id of the exit, or a safe place that otherwise wouldn't be obviously safe. Or maybe you've decided the tile in front of you is unsafe and you want to save that knowledge somewhere.

<p align="center">
  <img align="center" src="/assets/2018-08-17/robo-current-location.png" title="No, the new artwork is not a question mark." />
</p>

So location ids have vital use cases. But seeing _`safe_tiles[]: 5435, 8823, 1278`_ decorating your code tells you only that you have 3 ids, not where they are or, perhaps, that your algorithm that selected them is not working properly.

So I've had an idea for quite a while now that we take a look at the current stack, ie all the values of the running program, and highlight locations with the variables & sequences that are bound to them. This way when you save a location you'll actually _see_ it in the world.

Take for example the first time you encounter data points in the game. The data point contains a location id, in this case it's the exit to the level.

<video src="/assets/2018-08-17/key-without.mp4" controls></video>

So we're checking the edges to see if a location matches the one we ***robo_use()***-ed. That means we need to save at least one location in a variable, in the video I called it ***key***. And you can see it flip from ***0*** to ***1148*** in the first level. If we were then to highlight the stack locations, we should _see_ ***key*** in the world somewhere.

<video src="/assets/2018-08-17/key-with.mp4" controls></video>

Cool so you can see the location lit up it bright placeholder neon now. It's important to note this **isn't** saving the special location from the data point and highlighting it for the player. This is highlighting the locations that the player has saved in their stack, for whatever reason. It's a tool to understand your own algorithms, what's going on & what's going wrong!

Eventually it'll have the variable or sequence name highlighted alongside, so you can clearly see what variable contains a highlighted location. I'll also need to come up with a way for it to be there without destroying the art underneath. But even in it's current placeholder paint-on-the-level form it can give an interesting visualisation of a solution.

Take this later level, I kept track of tiles I deemed safe one sequence and unsafe in another. So we should see two separate colours highlighting the world.

<video src="/assets/2018-08-17/paint.mp4" controls></video>

Really cool to see what was seemingly random spinning round the level become vividly clear as an exercise in determining a safe route forward to the exit. You can even see the yellow highlight of the tile in front before the algorithm deems it safe or unsafe.

The hard parts of the highlighting are now done, hence seeing it working. It needs polishing and work to make it not too visually overpowering while still clear and useful. This should be a really nice tool though. Helping you when the solution isn't quite working & satisfying when it finally paints the level all the way to completion.

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/9847j0/robo_instructus_painting_the_stack_upon_the_world/) | [twitter](https://twitter.com/bigabgames/status/1030505117420797952) | [facebook](https://www.facebook.com/bigabgames/posts/2029821083771935)
