---
preface: robo-2
title: GPU Texture Compression
excerpt_separator: <!--more-->
---

After a week of reading, experimenting and screwing up my face into a slightly disapproving thinking shape; **beta-1.7** update is here and it's bringing GPU texture compression.

![](/assets/2019-04-12/top.jpg "BC3 compressed max quality textures for all")
<!--more-->

The benefits of GPU compressed textures are much reduced VRAM usage, comparable to using _Textures: Low_ while retaining high quality comparable to _Textures: High_. On top of this the game load speeds are hugely reduced now the textures no longer require processing before sending to the GPU.

So that's the benefits. On the other hand I almost didn't bother adding it at all. The game's rendering library _gfx-rs (pre-ll)_ doesn't support texture compression. So I had to reach into the murky waters of OpenGL myself.

The following is a short story on what development is actually like.

## Texture compression, which one?
I started looking into this knowing only that the game's textures were stored on the GPU uncompressed, unlike the game's PNG files. This caused large VRAM usage that was only going to get worse as more assets are added to the game. I also knew texture compression was a thing on GPUs and not really a new thing.

It turns out there are a bunch of different GPU compression techniques, generally having multiple names each in case you weren't confused already. I first starting looking at [ETC2](https://en.wikipedia.org/wiki/Ericsson_Texture_Compression) compression. This had the two compression variants I was interested in 8-bit sRGB & sRGBA. It also seemed well supported. I didn't use it in the end, but I'll get to that later.

## Getting compressed textures into the GPU
Gfx-rs doesn't support compressed textures. Time to look at the [gfx code](https://github.com/gfx-rs/gfx/tree/pre-ll) again & read about [glCompressedTexImage2D](https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/glCompressedTexImage2D.xhtml) & friends.

Maybe I should give up ***1***. This is the first point where I wonder if this is worth doing _at all_. I might be better served by living with the VRAM issues and doing something else.

On the other hand let's give this a go, I think I can handle this. I'll just implement a new texture format and link up a bunch of OpenGL calls. Now how do I test this?

## Compressing textures
First I need to actually turn my PNG files into compressed ones, this means finding some compressor project that can do this. More research, lead me to some projects like _google/etc2comp_ and then finding some build that I can use on Linux. With that I can produce a _logo-etc2.ktx_ file that was compressed and ready to be uploaded. Great, so let's upload it!

<b style="color:red">GL_INVALID_VALUE</b>

Oh dear it doesn't work, let's see if I can dig deeper to see why

> _GL_INVALID_VALUE: generated if imageSize is not consistent with the format, dimensions, and contents of the specified compressed image data_.

So the data I'm trying to upload is invalid. Any clues to how i might fix th-

<b style="color:red">GL_INVALID_VALUE</b>

Yes good point OpenGL, thanks for the help. Hmmm maybe I should give up ***2***.

## Understanding file formats
On the other hand, what's this _ktx_ file anyway? Maybe it isn't just the texture data. If it's got some header bytes that might be causing the problem. So I found the [KTX file format specification](https://www.khronos.org/opengles/sdk/tools/KTX/file_format_spec/), it's not too bad actually maybe someones already implemented it in rust... no. So I'll just parse according to the spec myself, maybe then it will work? Or maybe I should give up ***3***.

On the other hand parsing a byte spec might be "fun", let's give it a go. Yes! Wait no... Ok now it seems right. So the tail bit is the texture data, let's try sending that tail bit instead....

<p align="center">
  <img align="center"
  src="/assets/2019-04-12/logo.png"
  title="It actually worked" />
</p>

It actually worked! I am invincible.

## VRAM usage
Finally all the work has come to something. Now I can convert some of by big PNG files into ETC2 KTX files and let's see what difference it makes to VRAM usage!

It made no difference. **No** difference. How can it make no difference to VRAM usage? In investigating I stumbled onto a phoronix article from 2016 [AMD Polaris Doesn't Support ETC2](https://www.phoronix.com/scan.php?page=news_item&px=AMD-Polaris-No-ETC2). You see the OpenGL driver **does** support ETC2, it's just the hardware doesn't so the driver presumably just decompresses and sends it to the GPU.

This is a bit of a downer, maybe I should give up ***4***.

## Choosing another compression option
On the other hand, maybe a different compression option will work better. I found most texture compression techniques have quite bad support in GPUs even many years after they appear. https://opengl.gpuinfo.org/listcompressedformats.php makes quite grim reading, you can see that only really ETC2 and one other compression format enjoy decent support in drivers. And I already found out the hard way that ETC2's story isn't as rosy in actual hardware.

So I opted for the oldest technique with the most names: **S3TC** or **DXTC** or **DXT1/DXT5** or **BC1/BC3** these all pretty much mean the same. These are around 20 years old and very well supported in hardware, but they can be a bit hard to use because they're not in core OpenGL. Why not? Because of a patent. This patent finally expired last year but the damage is still visible. Suffice to say I take a dim view of this.

## Compressing textures 2
So how do I compress to BC1 & BC3? Well eventually I did find an excellent project that does just that: [GPUOpen-Tools/Compressonator](https://github.com/GPUOpen-Tools/Compressonator). It has a cli that can compress a bunch of different formats into, among others, KTX files.

```sh
# compress logo.png -> DXT5/BC3 + generate mipmaps to .ktx format
CompressonatorCLI -mipsize 1 -fd bc3 logo.png logo-bc3.ktx
```
This tool turned out to be quite easy to use and worked well and fast. With it I can compress all my PNG files to BC1 (RGB) or BC3 (RGBA) KTX files with mipmaps.

With mipmap data huh, I wonder where that goes in the KTX file?

<b style="color:red">GL_INVALID_VALUE</b>

Shush OpenGL, yes I see the mipmap data goes on the end in order. I can fix this!

## VRAM usage 2
**Finally**, I convert a bunch of PNGs into BC1/3 and see a huge reduction in VRAM usage. I also see a huge reduction in loading time as previously I had to convert the PNGs into uncompressed RGBA data for upload and now the data is already pre-prepared for upload. This makes a big difference and will actually help me develop faster as the game is much quicker to re-load.

I can also get rid of the other texture options, everyone should be able to enjoy the full sized textures now they take up much less VRAM.

Out of all this I found out another little surprise that OpenGL has in store.

## OpenGL max texture width?
The latest gift from OpenGL I discovered this week is that drivers have a number, ie **16384**, called ***GL_MAX_TEXTURE_SIZE***. If you try to use a texture with width or height larger than this it won't work. No not the size of the texture in bytes, or even the size of the texture in pixels. Just the width or the height.

As soon as I discovered this I realised _this_ was the cause of some player's game crashes. My testing PCs have the value **16384** and my largest texture was ~12000x300 pixels so no problem. But if we take a look at what other people have we can see **8192** is **very** common. **4096**, **2048** are not unknown either ([https://feedback.wildfiregames.com/report/opengl/feature/GL_MAX_TEXTURE_SIZE](https://feedback.wildfiregames.com/report/opengl/feature/GL_MAX_TEXTURE_SIZE)). For anyone with these lower values the game will have crashed using _Max_ sized textures.

Is my game just destined to crash for some people?

All this messing about with compression actually provided quite a neat solution. I can query this value and if the texture is too big I can use mipmap data instead (ie multiple 1/4 sized levels down to ~1px). This essentially means I can totally avoid this crash. Using Compressonator it's really easy to generate the mipmap data, and using my own KTX logic it's really easy to access mipmap levels independently. This solution really fell into place nicely!

The other thing I did was to square up my sprite sheets more, I reworked the wide ~12000x300 sheets into ~2000x2000 with some extra work to eliminate filtering bleeding between the sprites. This should mean almost everyone gets the highest quality images, and the rest just get slightly reduced quality images.

## Conclusion
After all this work I have game that will load faster, run faster on more hardware and not crash where before it did. But it was kind of hard work that didn't leave a lot of room for much else in today's [release notes](https://github.com/big-ab-games/robo-instructus/releases/tag/beta-1.7).

Related:
* My ktx crate: [github.com/alexheretic/ktx](https://github.com/alexheretic/ktx), [crates.io/crates/ktx](https://crates.io/crates/ktx)
* Gfx-rs BC1/BC3 support PRs [gfx#2733](https://github.com/gfx-rs/gfx/pull/2733), [gfx_gl#38](https://github.com/gfx-rs/gfx_gl/pull/38)
