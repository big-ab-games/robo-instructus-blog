---
preface: robo-2
title: VRAM Usage & Error Tracing
excerpt_separator: <!--more-->
---

For today's **beta-1.6** update I've spent some time getting to the bottom of a game panic _(spoiler: VRAM allocation)_ and fixing the game's Windows error logging in the process.

<p align="center">
  <img align="center"
  src="https://user-images.githubusercontent.com/2331607/55616270-57ff5c80-5789-11e9-9f2e-6cb20b6a38fb.jpg"
  title="New Textures setting" />
</p>

<!--more-->
## VRAM usage
The game is 2D without a huge amount of textures, and as such I hadn't put too much thought into VRAM usage. Surely it'll be fine right? However, with GPUs it's very easy to use more VRAM than you think or to tank the FPS with a sloppy shader.

For example a PNG file may only be 10MB but when uploaded to the GPU it becomes a lot bigger as GPUs need to store images in a random access friendly way. In my case this means uncompressed, as more work needs to be done to investigate GPU texture compression. So the game assets can take up a large amount of video memory.

![](/assets/2019-04-05/robo-walk.png)

As new effects are being added to the game, these are new sprite animation sheets that take up yet more VRAM. To combat this I've added a new ***Textures*** setting in the game's video menu. This allows simply using lower texture sizes which of course reduce video memory usage.

In testing different settings I found my current textures to be generally over-large. I could reduce many textures to 25% of their size without visible loss of quality in game. This is a large reduction indeed, though some parts of the game (level selection background) were more sensitive to this reduction. The more sensitive areas can still be reduced by 50% with minimal loss of image quality.

I could test the game's VRAM usage really well using `GALLIUM_HUD=requested-VRAM` in Linux. In a simple test loading a bunch of the game's assets I found the game requests almost 700MB of VRAM with the full size textures. My optimised reduction of textures became a new default _High_ setting and a more extreme 1/16th size is a _Low_ setting for reducing the texture sizes further at the cost of image quality.

Let's take a look at _Low_, _High_ & _Max_ texture sizes rendered at a high resolution.

![](/assets/2019-04-05/all.webp)

Particularly obvious is the _Low_ setting. The difference between _High_ and _Max_ is more subtle even at high resolution. But you can probably see that _Max_ is sharper.

Game requested VRAM:
* Max **680 MB**
* High **270 MB**
* Low **160 MB**

Despite _High_ being nearly as good as _Max_ it has hugely reduced video memory usage. It's so much better than I actually disabled the _Max_ option at 1080p and below. To see why lets look at _High_ vs _Max_ at 1440p.

![](/assets/2019-04-05/1440-high-max.webp)

Yes this is an animation it is actually changing. You may be able to see some of the shadowy texture darkness changing a bit. This should show that _High_ is a great default setting for almost everyone. If you want to use _Max_ for your 4K or greater display make sure you, well you should already, have at least 2GB of VRAM.

## Error tracing
In the worst case high VRAM usage can cause the game process to "panic", quitting the game and printing an error to the _error.log_. Panics like these in general should never happen. In some truly exceptional cases they are unavoidable, in other cases they are rare enough that the cost of handling them without panicking isn't always worth it.

But this week debugging a Windows panic that was ultimately caused by VRAM allocation failure I found my _error.log_ traces to be not much help.

```
(main) stack backtrace:
   0: <no info> (0x13f9bd4bd)
   1: <no info> (0x13fdbda35)
   2: <no info> (0x13fdbd544)
   3: <no info> (0x13fdbd429)
  ...
  16: <no info> (0x13fdbdd42)
  17: <no info> (0x13f84d4f7)
  18: <no info> (0x13fdd4bd8)
  19: BaseThreadInitThunk (0x76fe59cd)
```
The bits that say `<no info>` are the bits that are supposed to help me, with info. When I first introduced the _error.log_ I started including debug symbols in my builds so that traces like this could actually be helpful. And yes, I did test this on Linux and on Windows.

However, on Windows it seems the debug symbols are not embedded in the binary. They're actually in a _robo_instructus.pdb_ file linked to the exe by an **absolute path** to where this file was generated. This means I can package up the exe, move it about and test it on my machine without issue. But as soon as I take the exe elsewhere, like **any of my players** the .pdb will not be available.

To solve this I linked the binary to a relatively positioned pdb with `cargo rustc -Clink-arg=/PDBALTPATH:robo_instructus.pdb` and packaged pdb alongside the exe. This fixed the issue testing on another computer. However, when testing in Steam the traces were still lacking info. I found that the default steam build configurations include a _*.pdb_ exclusion, hmm. With that removed the traces are in, and future panics can be fixed with proper haste.

I honestly don't like leaving my nice rust world of things working exactly as I imagine they will. The above is an example of where Linux is much better than Windows currently for rust binaries, the debug symbols are simply embedded in the binary.

## New stuff
Of course, beta-1.6 brings other stuff too. Improved error message, new effects and fixes. See the [full release notes](https://github.com/big-ab-games/robo-instructus/releases/tag/beta-1.6).

<p align="center">
  <img align="center"
  src="https://user-images.githubusercontent.com/2331607/55617370-d4933a80-578b-11e9-99c6-35403069ac43.jpg"
  title="New robo_location(),robo_forward_location() effects" />
</p>

I've also made improvements to try to prevent any chance of save data loss caused by the game itself even if killing or OS crashing while the game is running. Tip of the week, renaming on Windows (specifically rust _fs::rename_) is **not** atomic. Would everyone please just install Linux?
