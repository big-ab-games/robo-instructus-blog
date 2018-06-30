---
preface: robo
---

While the alpha is getting closer, twist; The title is actually referring to this weeks work including _wrapping the code that you write in the game_ so it fits in a given width. The title-interpreting-rug that was beneath you, look down. It is gone.

### Wrapping

[![](/assets/2017-09-01/wrap.png "Wrap wrap wrapping!")](/assets/2017-09-01/wrap.png)

Code wrapping is what happens when terrible programmers write lines that are too long. Horizontal scroll bars are basically the devil, so wrapping steps in to derive order from chaos. Check out the little ↳ icon which indicates the line is wrapped. We also maintain the indentation, which is nice as indentation matters. It also handles cursor movement nicely, and code execution highlighting!


In a way this is an edge case, but an important one. The in-game language, *badder*, does not support explicit line splitting for simplicity. So nice visual wrapping is actually necessary, and this is why I've made sure it's in the alpha.

<div class="video-wrap">
  <iframe width="560" height="315"
    src="https://www.youtube-nocookie.com/embed/hk8LoHqHkGI?rel=0&amp;start=24"
    frameborder="0" allowfullscreen></iframe>
</div>

### Scrolling
Another way mischievous programmers (*wrapscallions*, if you will) annoy text rendering windows is by writing too many lines of code. Most programmers prefer to see the code they're writing, so I've added scrolling.

<video src="/assets/2017-09-01/scrolling.mp4" controls loop autoplay></video>

I went for a minimalist auto-hiding scroll bar. You scroll with the mouse wheel, or cursor movement. It represents the size of the current view and pretty much works as you would expect, with the bar rendered as a single OpenGL quad.

<div class="video-wrap">
  <iframe width="560" height="315"
    src="https://www.youtube-nocookie.com/embed/RXhu26jEmZY?rel=0"
    frameborder="0" allowfullscreen></iframe>
</div>

These are two important features I could add because I've switched to my own glyph rendering library [gfx_glyph](https://github.com/alexheretic/gfx-glyph). *I talked a little about that [last week](/2017/08/25/wrangling-glyphs.html)*.

Currently I'm mid way through adding a proper level-complete dialog. I'm going to show some stats about the solution, i.e. how long it took. In future I want you to be able to see your stats compared with the world, so you can feel bad after you feel good.

### Alpha plans
As mentioned last week the tutorials remain the biggest alpha feature yet to be completed, and otherwise I'm very close. The first alpha will be limited to a small audience so I can eliminate the most pressing issues & bugs. Ultimately I'll release an open alpha to gather as much feedback as possible from as many people as possible and hopefully build interest in this game.

When I release the open alpha I'll really need the help of everyone to promote it, if no-one hears about it no-one will test it! If you want to help test the very first alpha please [contact me](mailto:alex@roboinstruct.us). Of course, I'll be talking about it more and more as we get closer.

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/6xdzww/robo_instructus_wrapping_up_the_alpha_code/) | [twitter](https://twitter.com/bigabgames/status/903584009879523329) | [facebook](https://www.facebook.com/bigabgames/posts/1576325825788132)
