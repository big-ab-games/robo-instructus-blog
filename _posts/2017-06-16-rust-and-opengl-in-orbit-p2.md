---
title: Rust And OpenGL In Orbit Part 2
---
Continuing to look at an initial game demo project of mine, a 2D orbital body sim, lets discuss user interaction. For this demo the interaction I'm interested in is moving about, zooming in & following bodies. How do we make this sort of thing powerful and natural?

If you missed part 1 [read it here](/2017/06/09/rust-and-opengl-in-orbit.html).

### Moving About
What I want is for left-clicks to make the cursor 'glued' to the world allowing me to drag around my view.

<video src="/assets/orbit-p2/dragging.webm" loop controls></video>

To achieve this I listen to the mouse movements when left-click is down and adjust the view center. The demo starts at *(0, 0)* so if you click and move the mouse down a little the origin will perhaps become *(0, 2.1)*.

A complexity of this is that the mouse events will give you movement in *pixels*, but my origin is a co-ordinate of the Alexverse. To make the cursor 'glue' to the Alexverse I need to translate pixel distances to world distances perfectly\*. Don't forget that the zoom can change causing this translation to change. This kind of translation is fundamental to interactive graphics.

### Zooming In & Out
Naturally I'd like mouse scrolls to change the zoom. So scrolling forward should bring the orbital bodies closer. At first this may seem trivial, have a zoom multiplier number and change it by an amount when the user scrolls.

<video src="/assets/orbit-p2/bad-zoom.webm" loop controls></video>

However, this is kind of rubbish:
1. Scrolls jumps seem too big when close up & too small when far away.
2. Scrolls only jump into & out of the center, they don't pay attention to where the mouse is. This doesn't feel natural.
3. Why are scrolls jumping anyway? They should be smooth.

For all these issues we can look at somewhere that's done this better, e.g. [Google maps](https://www.google.co.uk/maps/@30.1590487,-30.1284594,3z). The solutions are specific but feel so natural that I'd never thought about them specifically before.
1. Notice how zooming adjusts based on our distance from the ground. We can zoom out quickly to see the world, but also zoom just a little more in on Big Ben. So the zoom-factor changes based on our distance to the ground.
2. Zooms move toward the cursor somewhat, or away when zooming out. More specifically the cursor remains 'glued' to the world position while zooming.
3. The transitions in zoom are animated and don't simply jolt into each other. This can be important, as the transition helps the user track where their new view is.

#### Solving 1 & 2
I addressed **1** by doubling/halving the zoom for each scroll, this is exponential increase/decrease provides a lot of movement when far away, and more subtle control closer up. For **2** when changing zoom look at where the cursor is, where it ends up and adjust the origin with the difference.

<video src="/assets/orbit-p2/better-zoom.webm" loop controls></video>


#### Solving 3: Smooth Transitions
Finally we want our zooms to be smooth and animated. So the zoom should change into our intended zoom over, say 1 second, instead of instantly. The simplest way of doing this is each frame check how much time has passed if say 0.7 seconds has passed we should zoom `0.7 * zoom_factor` in. After a second we'll be zoomed in fully to our intended zoom. This presents new problems
* We need to make sure we don't screw up **2** as we're transitioning to our new zoom, so the cursor must stay in the correct position all the time.
* What if we scroll during a zoom transition?

Even worse I soon noticed the animation felt *wrong*, it seemed like the transition was too slow at first and too fast at the end.

#### Easing
To make the zoom feel *right* we need to abandon the previous zoom transition and transition using [easing](http://easings.net). In short an easing function describes a way to transition between two values. There are a whole bunch of commonly used ones *ease-in-elastic*, *ease-out-cubic* etc, they're straight forward to implement in any language. Actually the method I described above is *linear easing*, and it isn't too surprising it doesn't work out with an exponential zoom.

After generalising my code to use any given easing function, and messing about with them (using elastic for zoom was fun) I ended up using the exponential ease out function.

<video src="/assets/orbit-p2/easing-zoom.webm" loop controls></video>

Next week I'll look at rendering the orbital path of these bodies in nice curved lines.
