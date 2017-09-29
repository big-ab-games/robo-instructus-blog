---
preface: robo
---

This week I've been improving the story & tutorial sections of Robo Instructus, focusing on the tech behind it being flexible. I need pictures and fancy fonts to properly explain to you what's happening. I also need these to render on your crappy old screen.

![](/assets/2017-09-29/exit-info.png "Get to the chopper!")

### Mixed text
One thing I wanted was mixed font layouts of text. I want to show you the new functions *names* rendered in just like they would be in the game. But the function *descriptions* using a normal font. So that means a mix of mono-spaced coloured text alongside sans.

To do this without manual hacks I expanded my rusty glyph rendering library [gfx_glyph](https://github.com/alexheretic/gfx-glyph) with new code to handle layouts with multiple fonts, scales & colours inside them.

![](/assets/2017-09-29/code-and-text.png "Coloured mono + sans all in one layout")


### Fast development
I anticipate changing these story/tutorial sections many times during the alpha's development, so full flexibility is important. I've created a stripped down markup language that I write the pages in. This way I can quickly create & modify pages of info, all without re-compiling.

### Images & re-sizing
Rendering images isn't difficult. But I had a little work getting them nicely loading dynamically from my markup and automatically sizing to fit on the screen. This is important for the game to support all resolutions.

I've actually designed pretty much all aspects of the game to support dynamic sizing based on resolution. Even the alpha should support any fullscreen or windowed configuration. Later I'll add user tweaking of font size etc.

### A peek at development
Why don't we zoom out the normal movie a bit and see my dev environment. Lets look at how I'm writing these story/tutorial pages, and how the auto sizing is going.

<video src="/assets/2017-09-29/info-development.mp4" controls autoplay loop></video>

*Note: The big red crosses are just images I haven't added yet.*

As you can see the pages now have some nice properties.
* Images are dynamically loaded and rendered in a center alignment
* Images are resized if the page doesn't fit in the screen, this allows me to use high-res images later and for them to work on all resolutions.
* All game text and UI scales according to resolution. Again this allows the game to support Ben's 8K mid-life crisis, and Joanna's death-bed straddling 1024x768 CRT.
* Content and size can be loaded on the fly, rather than re-compiling or even restarting the game. This just lets me work faster and tweak more easily when I'm improving these screens.

I still have content to add, but now should be unblocked to do so. Once I've finished the tutorials, checked Windows performs as well as Linux, and sanded off a few more rough edges the first alpha build will be ready for testers.

**If you'd like to help me test the incoming very first version please get into contact using one of the methods on the [front page](/)**.

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/738ltm/robo_instructus_information_for_all_resolutions/) | [twitter](https://twitter.com/alexbutlergames/status/913789221520977921) | [facebook](https://www.facebook.com/alexbutlergames/posts/1609596722461042)
