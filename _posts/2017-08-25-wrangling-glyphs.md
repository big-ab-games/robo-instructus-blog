---
preface: robo
---

I thought about it for several moments, but I can't think of any interesting way to say it. So I'll just come clean. I've been spending much of this week working on *text rendering*.

Still reading huh? Well text is not exciting, but it's still very important. Particularly for Robo Instructus as players will be writing and poring over text perhaps much more than most games. And actually text rendering in OpenGL is more difficult to handle than you might think. My previous solution was a library based on *freetype*, this required external dependencies and for whatever reason didn't seem to render quite the same way in Windows & Linux. It also performed quite poorly in debug mode, which means it just slows down my development.

To address my issues I spent a little time writing [gfx_glyph](https://github.com/alexheretic/gfx-glyph); a new open source rust library for fast text rendering. This uses a pure rust alternative to freetype so eliminates external dependencies. It also performs much better than the lib I was using previously. The debug performance of Robo Instructus is now good enough to develop & test under which is very nice! I hope the library will also prove useful to many other rust game projects.

[![](/assets/2017-08-25/gfx-glyph-s.jpg "rendering 100,000 glyphs pretty quickly")](/assets/2017-08-25/gfx-glyph.png)

### Resurveying the tools
A month ago [I explained many of the tools available to the player in the upcoming alpha](/2017/07/21/solving-problems-like-an-engineer.html#surveying-the-tools). Let's check out the newer ones. These tools provide the real weapons against the puzzle the alpha will present ***'which unknown tiles are safe?'***.

* `robo_current_location()` & `robo_forward_location()` functions that provide a unique id for the current tile and tile in front respectively.

  <p align="center">
    <img align="center"
      src="/assets/2017-08-25/robo_location.png"
      title="Give a tile a name... well a number anyway" />
  </p>

* `robo_detect_adjacent()` tells us absolutely the total number of tiles adjacent to the current position. This will work even if the tiles are unknown. This is the first real tool in cutting through to the truth. So in the below situation if we got ***2*** we could eventually conclude that the unknown tile here is in truth a real tile.

  <p align="center">
    <img align="center"
      src="/assets/2017-08-25/robo_detect_adjacent.png"
      title="At last, a light in the darkness!" />
  </p>

### Tutorials

A big task yet remaining is tutorials for the alpha. This is a big potential stumbling block as I need to make it informative enough to those with little coding experience, and yet not totally dull (my experience of most programming tutorials). On the other hand, a tutorial should be something I can improve based on feedback from the alpha. So I'll probably try to keep it brief and fill in the gaps later.

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/6vyd5w/robo_instructus_high_performance_text_rendering/) | [twitter](https://twitter.com/bigabgames/status/901070347876913153) | [facebook](https://www.facebook.com/bigabgames/posts/1567556503331731)
