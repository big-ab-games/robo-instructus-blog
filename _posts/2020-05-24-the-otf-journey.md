---
preface: robo-3
title: "Otf Font Rendering or: How I Should Have Learned To Stop Worrying And Love The TTF"
excerpt_separator: <!--more-->
---
While developing Robo Instructus I spent an inordinate amount of time messing about with text rendering. After releasing the game last year, I'd thought my time diving into the glyph filled rabbit hole of _text_ would be over... This was not to be, my text-retirement came to an end with a thought:

> **How hard can it be to get otf fonts working?**

![](/assets/2020-05-23/top.png "glyph_brush text rendering")
<!--more-->

Robo Instructus is quite a "low-level" game in terms of it's technology. It uses it's own custom OpenGL engine written in rust. If you make a game like this then rendering text is not solved for you. You have to roll up your sleeves or find a library. Back in 2017 the libs that were available weren't good enough in terms of features or performance. So I made my own [glyph_brush](https://github.com/alexheretic/glyph-brush). I wrote about some of the technical details of that in 2018.
* [Technical Look At Text Rendering In Robo Instructus](/2018/05/18/technical-look-at-text-rendering-in-robo-instructus.html)
* [Faster Screen Text Rendering](/2018/05/25/technical-look-at-text-rendering-in-robo-instructus-ii.html)

glyph_brush itself was based on a cool library that _was_ available at the time [rusttype](https://gitlab.redox-os.org/redox-os/rusttype). rusttype handled the manipulation & rasterization of individual glyphs but only supported ttf fonts, so glyph_brush only supported ttf fonts. So I just used ttf fonts in Robo Instructus and all was well.

## The crease in the sheet
In the later stages of development I was looking at supporting other languages, like Russian, but I found that not all the fonts I used could support things like Cyrillic glyphs & Chinese. For the latter I used a whole separate set of fonts. For Russian I found a replacement font quite similar to what I was using for English (Exo.ttf) that _did_ support Cyrillic glyphs: **Exo2.otf**.

Of course, the hitch was this was an otf font and it didn't work with rusttype. At the time I found that adding otf support to rusttype meant tackling a whole bunch of stuff that I didn't really understand. Parsing the font files themselves isn't at all trivial, and didn't look fun at all the code rusttype used was a mess of magic numbers. I didn't fully understand rusttype's rasterization logic either, but I could see it only supported lines and quadratic curves. To support otf it would need to support [_cubic bezier curves_](https://en.wikipedia.org/wiki/B%C3%A9zier_curve).

![](/assets/2020-05-23/q-c-beziers.png "left: ttf, right: otf")

This was a bit much at the time. I decided to forget about all this and just use the best ttf fonts I could find and get the game done. So I did exactly that.

There were no complaints at the lack of cubic beziers in the games text. There were no issues in glyph_brush's or rusttype's repos asking for otf support. All was well.

Except I didn't forget. This stuck in my mind as a crease in the sheet I couldn't flatten yet. I had a vague ambition to "solve" this after the game's release.

## The call to arms
In mid 2019 [an issue](https://gitlab.redox-os.org/redox-os/rusttype/issues/137) appeared in rusttype's repo about a new font parser crate [ttf-parser](https://github.com/RazrFalcon/ttf-parser) that could parse otf & ttf fonts. This presented a solution to half the problem, parsing the otf files properly.

When I tried migrating rusttype to ttf-parser I found more issues still. Just using it at all proved to be a challenge. I ended up having to handle a self-referential struct in rust, which isn't really very nice. Having to crack out the dreaded `unsafe` keyword is something I try to avoid if I can.

## Drawing cubic beziers
Enventually I did solve those issues and got rusttype working using ttf-parser, but the cubic bezier problem remained. I realised I just didn't understand rusttype's rasterization code. I'd written regression tests for it, benchmarks to track performance. I'd optimised it by removing hashing. But I'd never _really_ understood exactly what it was really doing.

This is a problem if I want to try to draw a more complex curve. I started looking around elsewhere to see if this problem has been solved by cleverer people. I remembered reading about [font-rs](https://github.com/raphlinus/font-rs) and it's fast rasterization. When I dug into the code I found it didn't support cubic curves either, but it was much smaller & nicer code compared with rusttype's rasterization. I mean I didn't understand it 100% either, but at least there was _less_ of it.

Rusttype was initially based on a c library [stb_truetype](https://github.com/nothings/stb/blob/master/stb_truetype.h) and I was also aware that this lib now supported otf. So I figured there must be some cubic curve logic in there somewhere... Yes what's this `stbtt__tesselate_cubic` that seems kinda cubic-y. If I squinted in the right way I could kinda see what it was doing too. It recursively approximated a cubic curve into lines.

This presented an opportunity to smoosh font-rs, which could draw lines & quadratic curves, together with stb_truetype's cubic curve approximation into lines (if I could translate that properly into rust). I was quite surprised when this actually worked. I had created [ab_glyph_rasterizer](https://github.com/alexheretic/ab-glyph/tree/master/rasterizer) that could draw all 3 kinds of curves I needed for ttf & otf fonts, and it was _fast_.

<blockquote margin="auto" class="twitter-tweet tw-align-center" data-theme="dark"><p lang="en" dir="ltr">Hey it actually worked! OTF font support thanks to ttf-parser and a new rasterizer I&#39;m working on that can actually render those pesky cubic beziers. Coming soon to rusttype, glyph-brush &amp; Robo Instructus.<br><br>Example: Exo2-Light.otf<a href="https://twitter.com/hashtag/rustlang?src=hash&amp;ref_src=twsrc%5Etfw">#rustlang</a> <a href="https://twitter.com/hashtag/gamedev?src=hash&amp;ref_src=twsrc%5Etfw">#gamedev</a> <a href="https://t.co/Q5OZxllGNX">pic.twitter.com/Q5OZxllGNX</a></p>&mdash; Big AB Games (@bigabgames) <a href="https://twitter.com/bigabgames/status/1247656705598590978?ref_src=twsrc%5Etfw">April 7, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## New sheets, new creases
I delivered otf support to rusttype 0.9 using ttf-parser & my new rasterization crate. During this work I'd also found that rusttype's API wasn't really ideal for otf performance characteristics. rusttype is eager to use pixel bounds for glyphs, for otf fonts (in general) this is quite expensive. This meant otf layout performance was kinda bad compared to ttf.

Designing rusttype to _not_ do this in a nice way was quite difficult. I ended up experimenting on a total rewrite to solve this and other performance issues I had with rusttype. [ab_glyph](https://github.com/alexheretic/ab-glyph/tree/master/glyph) was born, like rusttype but otf was as fast as ttf overall **~1.5-8.8x faster** than rusttype for laying out glyphs in a paragraph.

This was great, but more work and churn for the libraries downstream of rusttype/ab_glyph. I rolled up my sleeves and converted glyph_brush and finally Robo Instructus itself.

## The tragic reveal
Now, sometime after I'd got rasterization working for cubic curves I went looking for the **Exo2.otf** font that had ultimately been responsible for all this effort in the first place. I was going to be satisfying to see this font render now after all my work. On my search though, I found something **horrifying**. Next to the otf font folder i saw a ... **ttf** folder.

<p align="center">
  <img align="center" src="/assets/2020-05-23/exo2-dirs.png" title="Oh no..." />
</p>

Yes the entire Exo2 family is available in ttf. It probably was all along. I could have, _should have_ just downloaded and used these & shrugged my shoulders about otf years ago.

You have to laugh at yourself when you've not only moved mountains to achieve the following, quite subtle, change (which is kinda funny anyway) but after everything you could have done it without any real work.

<p align="center">
  <img align="center" src="https://user-images.githubusercontent.com/2331607/82735754-e7642800-9d1b-11ea-9a8f-d38a3621a1ea.gif" />
</p>

At the end of the day otf support is still nice to have in the stack. I hope others find it useful. And if you ask, did I use the Exo2.ttf or Exo2.otf in the end? The bloody **otf** one of course!

##### Comment on [twitter](https://twitter.com/bigabgames/status/1264557215693918209) | [reddit](https://www.reddit.com/r/rust_gamedev/comments/gpsrkz/otf_font_rendering_or_how_i_should_have_learned/)
