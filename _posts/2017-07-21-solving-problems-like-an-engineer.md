As I've been banging on about in previous weeks; I'm making this game about being an engineer. It's about inventing robot-logic to help a little bot defeat tricky mazes. It's also about not only thinking ***'how do I solve this puzzle?'***, but then figuring out ***'how do I articulate my solution into the robot's mother tongue?'***. Once done, you'll watch it succeed or fail. You'll tweak, and change until it is satisfactory.
<br/><br/>If you can do all this, you'll be an engineer, my son!

### Surveying the tools
First step is looking at the level and checking out the obstacles and the tools available.

![](/assets/2017-07-21/look.jpg "A level with some basic tools documented")

So we can see our goal, the green tile. We can see we start at the bottom. Dark tiles are unknown, they could be unsafe and we don't want to fall off the edge.
The solution is easy here, we just walk the safe tiles to the exit... Well, easy for *you* maybe. However, it's *your robot* that will have do it. So let's take a look at the robot's tools:
* `robo_left()` A function we can call to move to the next side of the current tile (counter-clockwise).
<br/><br/>So 3 calls would put as back where we started (note **Placeholder Panda**, aka *'Double-P'*, isn't properly animated so always seems to face us, so use your imagination a little, I can't do everything *...yet*).

  ![](/assets/2017-07-21/robo_left.png "Turning about. It's 'left' as he's meant to be facing the other way")
* `robo_forward()` Moves to the tile 'in front'. Also veers right because triangles only have 3 sides.

  ![](/assets/2017-07-21/robo_forward_1.png "Going forward is weird in triangle land")
  ![](/assets/2017-07-21/robo_forward_2.png "Going forward is weird in triangle land")

* `robo_scan()` Scans the tile in front, returning what it is, or that it is *unknown*. So ***1*** means we have a normal tile in front, ***2*** an exit tile, ***-1*** means there's nothing and ***-999*** means unknown.

![](/assets/2017-07-21/robo_scan_1.png "Good")
![](/assets/2017-07-21/robo_scan_2.png "Bad")

We can move about and we can test if it's safe in front, so it looks like we have enough to complete this level. How about a simple solution: **If it's safe in front we go forward, otherwise we turn left and try again**.

### Articulating the solution
Now we have an idea of a solution we need to start explaining the plan to Double-P. This is when we become an engineer!
```rust
loop
    if safe_in_front()
        robo_forward()
    else
        robo_left()
```
Don't just skip over that code, take a proper look. *Go on now...*

Can you see how its the same as our plan? But it's written in the language the robot can speak. We missing one thing, I just made up ***safe_in_front()***. So we need to implement what that actually does.
```kotlin
fun safe_in_front()
    var scan = robo_scan()
    scan is 1 or scan is 2
```
Remember ***robo_scan()*** gives us ***1*** for a normal tile, and ***2*** for the exit. So if either of them are scanned we consider it safe, and this function will return non-zero. Now let's see if she works!

<video controls style="width: 100%">
  <source src="/assets/2017-07-21/solution-600k.webm" type="video/webm"/>
  <source src="/assets/2017-07-21/solution-600k.mp4" type="video/mp4"/>
</video>

Hey it works! Lovely stuff, the crowd goes wild.

Did you also notice the visualization as it was running, the funny flickering highlighting? This is part of the interactive feedback that I'm building to make the experience more satisfying and immediate. I've made some nice advances on there in the last week, but I've gone on long enough, so I'll write about that another time.

### Other progress
I've successfully merged my Linux/XWayland support patches upstream so now can run the game properly in an X11 or Wayland session. I've also been working on improving my font/text rendering code to improve performance there as the game will be text heavy and I'm not totally satisfied with my current library's showing.

Broadly my work continues onwards toward the playable alpha-demo, and everything I'm doing is about achieving that. Check back next Friday for more progress.

##### Comment on [twitter](https://twitter.com/bigabgames/status/888413995283120130) | [facebook](https://www.facebook.com/bigabgames/posts/1514848191935896) | [reddit](https://www.reddit.com/r/devblogs/comments/6oogxx/that_guy_that_quit_his_job_to_make_games_solving/)
