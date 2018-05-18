---
preface: robo-2
---

Robo Instructus is a game of writing instructional code for robots. Sometimes these robots are going to need a whole lot of text. Since the game is lower level than most, not based on an engine, I had to ferry my little letters from font byte data to graphics card vertices myself. Well, with a little help from my <s>friends</s> libs. Let's take a technical dive into that journey.

![](/assets/2018-05-18/main.png "Text!")

### The Idea
Robo Instructus uses a fairly simple idea of text rendering, you draw the required glyph (e.g. a single letter) into a grid of pixels with the CPU, this is called rasterization. Then send these pixels as a texture to the graphics card and tell the GPU where to put it on the screen with a bunch of vertex coordinate information.

This technique isn't the only way to go about getting text into people eyes. Also even the libraries I use are not unique in function. But instead of talking about _other_ ways of doing this I'm going to stick to how it's done in Robo Instructus' Rust & OpenGL stack.

### Font data
We start the journey with font data. A [font](https://en.wikipedia.org/wiki/Computer_font) defines for us the shape of each glyph. In particular Robo Instructus uses TrueType outline-fonts where the data describes glyphs in terms of lines and curves that can scale to any size. There are many freely available, for example the game uses [Deja Vu Sans Mono](https://dejavu-fonts.github.io/) for the code text.

So we download & use the _DejaVuSansMono.ttf_ file which contains nice looking glyph lines & curves. We have to decode the _ttf_ format to actually understand what those lines & curves are, then we need to do something with them.

The first letter of the code pictured above is **v**. We know the shape of the letter & where we want it so it's time to create a **v** texture.

### CPU Rasterization
Once we pick a position and size of our glyph the font will tell us exactly where the lines and curves are positioned. However, monitors are not perfect and basically display images by using a grid of lots of single coloured pixels. We can't render the glyph perfectly because for any single pixel we have to pick just one colour.

This pixel alpha is calculated by _coverage_. The more of the pixel is covered by the actual glyph vector the closer to full **1.0** alpha the pixel will be set to.

![](/assets/2018-05-18/v-rasterization.png "V shape rasterized to the pixel grid")

After rasterization we have pixel data in the form of an array of alpha values between **0.0** & **1.0**, a colourless texture that looks like our **v**.

The [rusttype](https://github.com/redox-os/rusttype) library is instrumental in handling these steps.

### Over to the GPU
Now we have texture information this is packed into an 8-bit alpha colour array and sent to graphics memory via OpenGL. We need to let the GPU know where to render this texture, and what bits of the texture to render.

This is done with a small program run on the GPU called a _shader_ & the data for this program: 6 vertices per glyph. Each vertex has:
* A screen pixel coordinate translated into an OpenGL _[-1, 1]_ coord.
* A RGB colour.
* A texture coordinate.

![](/assets/2018-05-18/v-vertices.png "V glyph vertices")

_6 vertices_, rather than 4, because OpenGL is big into triangles.

[gfx-rs](https://github.com/gfx-rs/gfx/tree/pre-ll) is used to conduct this OpenGL communication with the GPU.

### Impacts
This style of rendering is in many ways fairly primitive. Rasterization is normally done only on the GPU. It makes sense as this is a very parallel task suited to a graphics card. Using the CPU also means the pipe is quite rigid. We can't really use the same **v** texture for another **v** in a different sub-pixel position, because if the CPU pixel grid doesn't match the actual grid then the texture will be become blurred on the GPU rasterization step.

However, a positive of this is the simplicity of the GPU usage. This style of rendering requires very little from the GPU. The pipe is very CPU limited, but we can eliminate some of the issues with liberal use of caching.

### Performance & Caching
A naive implementation of CPU rasterization into textures for each frame would be very slow once a bunch of glyphs are on the screen. However, we can do better without throwing the whole technique in the bin.

First while not _every_ **v**-glyph can use the same texture because of sub-pixel position differences, many of them ***can***. If we could setup a single texture full of all the glyphs we need to render shared between similar-enough glyphs we can decrease both our need to rasterize on the CPU, and texture info to upload to the GPU.

Another thing; does text change that much from frame-to-frame? In general not so much, most of the time 1/60th of a second later the text is in exactly the same position. Exactly the same texture. Exactly the same colour. Which means we don't need to re-upload any texture info, we don't need to re-upload any vertices. We just ask the GPU to re-draw & blend, and because the GPU side is so simple this means **very fast** rendering.

These two kinds of caching _(along with layout-caching which I won't go into)_ are included in my own library [gfx-glyph](https://github.com/alexheretic/gfx-glyph) sitting on top of rusttype's **gpu_cache** to which I've personally made many optimizations & fixes. **gfx-glyph** allows me to have arbitrarily complex text layouts that, once baked & cached, are so fast they **don't impact frame time**.

![](/assets/2018-05-18/gfx-glyph-example.png "gfx-glyph rendering loads of stuff very fast")

### Future improvements
Since after they're baked the text rendering performance is excellent, I generally try to improve the worst case speed. That is the _baking_ time. This comes down to layout calculation, CPU rasterization etc. In future rasterization could be moved back to the GPU in a compute step, still making use of caching the result in a texture for fast drawing. Really it should render directly into GPU memory to avoid any uploading.

I've been continually making smaller performance improvements over many releases of **gfx-glyph**, **rusttype** & Robo Instructus itself. The end result is now I can render all the user-code, icons and in-game text without slowdown even with the rust-compiler in debug mode. The former gives a good experience for my players, the latter allows me to get the game done.

Speaking of which more Robo Instructus specific updates are coming up.
