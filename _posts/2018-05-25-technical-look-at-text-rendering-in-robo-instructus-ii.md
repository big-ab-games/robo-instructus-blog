---
preface: robo-2
title: Faster Screen Text Rendering
---

[Last week](/2018/05/18/technical-look-at-text-rendering-in-robo-instructus.html) I looked into how the text rendering pipe used to draw all the lovely text in Robo Instructus works. At the end of the article I mentioned performance. This style of text rendering can be slow. So how do we make is fast?

![](/assets/2018-05-25/w-screen.png)

## Pre-rendering Stages

Before the graphics card can render the text we need to compute the layout, ie where all the characters will go, rasterize the glyphs into textures and finally generate vertices.

### Layout
The layout stage may seem simple, there's no funky GPU business here. However, positioning text in a paragraph is harder work than it may seem. There is lots of complexity you may not have thought of, font kerning, unicode annex handling etc. This can actually be somewhat expensive for large bunches of text.

But eventually we'll have text turned into font glyphs scaled corrected and positioned on the screen.

### Texture
The texture stage is where we turn positioned glyphs into textures that we can render. This is the CPU rasterization process I talked about last week. Texture changes also need to be uploaded to GPU memory.

### Vertex
Finally with texture coordinates and screen positions for every glyph we can generate the 6 vertices per glyph that tell the GPU where to render what bits of a texture.

```
                    +--------+         +---------+         +--------+
"some text" ------> | Layout | ------> | Texture | ------> | Vertex | ------> GPU
                    +--------+         +---------+         +--------+
```

## Performance
Each of these stages have an noticeable impact on frame time, particularly the **texture** stage. Once we have a lot of text we're just not going to get acceptable frame rates from doing this all every frame.

Time to optimise! First lets tackle the worst area.

### Texture Caching
The library [rusttype](https://github.com/redox-os/rusttype) handles the text rasterizing. It also provides a texture cache data structure. This bad boy is going to step in and help our texture stage performance.

There's no point rasterizing the same glyph twice, so instead lets save the texture for use in future frames. And also multiple glyphs at the end of the layout stage probably look fine with the same texture so we can save work there too. In the end we can have a warmup cost where the bulk of the glyphs are rasterized and after that enjoy fast cached texture lookups.

Even if the text layouts change, after warming up we should have a decent index of rendered glyphs and be able to respond fast as long as our texture lookup is fast.

Actually since last week's article I optimised glyph texture lookups in rusttype to be around [3x faster](https://github.com/redox-os/rusttype/pull/111).

### Layout Caching
Most frames that are rendered will actually be the same text in the same place as last time. Why should we do the layout again. Caching this means we simply need to _hash_ the text data and if its the same as a previous layout just use our old work.

This means layout cost just disappears for most frames, but comes right back again if the text changes in some way. I could probably make use the cached layout in clever ways even after changes.

### Vertex Generation
2 triangles, 6 vertices are generated for each glyph. This is simple enough, but can impact performance. This also can be cached, as long as the previous stages have the same output.

There are always other ways to improve though, since last week I've cut 6 vertices down to **1 vertex per glyph** with the help of <s>geometry shading</s> instanced rendering. Basically 1 slightly fatter vertex is sent to the GPU and turns into the 4 corners we need. This alone actually improved worst-case performance by **18-50%**!

### Draw Caching
Taking layout caching further if _no_ layout has changed since last frame there almost isn't anything to do. All glyphs have already been rasterized, all textures & vertices uploaded. So skip all everything and just ask the GPU to draw again. Very fast indeed!

All this caching means text rendering is cheap most frames as we totally avoid hard work, and when we actually _do_ need to do something we only do a small part of the total work. This is why I love programming, this mentality is actually encouraged!

You can find the code for this heavily cached text rendering in my rust library [gfx-glyph](https://github.com/alexheretic/gfx-glyph).

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/8m3f4k/robo_instructus_even_faster_cached_text_rendering/) | [twitter](https://twitter.com/bigabgames/status/1000061351442698241) | [facebook](https://www.facebook.com/bigabgames/posts/1896458177108227)
