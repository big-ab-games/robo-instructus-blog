---
preface: robo
---

Robo Instructus alpha-1.4 is hot from the oven filling the room with the delicious smells of lovely new features. Two new major features arrive in this version and one of them is a biggun **rendering live stack values inline with code.**

![](/assets/2017-11-03/inline-stack-values.png "JUICE")

### Live inline stack values
Look at the code side of that image you'll see the the scan variable that ***robo_scan()*** returned is being shown inline *scan:&nbsp;-999*. This isn't part of the code that the player wrote, it's populated as the code runs. That's because it's really a live view onto the stack, that *is the programmatic memory of the robot*.

![](/assets/2017-11-03/inline-stack-values-focus.png "Knowing is half the battle")

It might not look like much right away, but you'll quickly find out this is a massive visibility boon for players and the more complex the player's solution the more helpful this becomes! I think it's going to be  hard to imagine this _not_ being there after everyone gets used to it.

Lets see it in action in a more complex later level, shall we?

<video src="/assets/2017-11-03/inline-stack-values.mp4" controls loop autoplay></video>

### Windowed & fullscreen
Until now the game has only offered fullscreen rendering, from *alpha-1.4* Robo Instructus supports windowed and fullscreen. You can toggle this in the menu. The window is fully re-sizable and all aspects of the game resize to suit the window size. However, the design is really meant for a large window compared to monitor size. Currently a small windows is treated exactly the same as fullscreen on a very small resolution monitor in term of scaling, and actually this makes it easy to test low resolutions.

<video src="/assets/2017-11-03/windowed-fullscreen.mp4" controls loop></video>

I think the game will be a good fit for windowed as I often go for maximized-windowed mode when playing puzzle games. Of course, the fullscreen option is still there. I may investigate moving that to windowed-fullscreen later, as it may provide benefits _we'll see_.

*If you fancy being a part of Robo Instructus' alpha testing get into contact with me using one of the methods on the [front page](/).*

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/7ajxqq/robo_instructus_a_window_to_the_stack_rendering/) | [twitter](https://twitter.com/bigabgames/status/926465112063533057) | [facebook](https://www.facebook.com/bigabgames/posts/1653412114746169)
