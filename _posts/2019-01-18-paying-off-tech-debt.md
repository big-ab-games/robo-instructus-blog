---
preface: robo-2
title: Paying Off Technical Debt
excerpt_separator: <!--more-->
---
Sometimes when developing software it makes sense to bosh out a quick and dirty solution to an issue and say "I'll improve this later". This is so common it's called technical debt. It allows focus to shift away from a less important feature until more vital stuff is done. However, It can be really tough to ever get rid of tech debt. You need to convince your boss to let you work on a new implementation of the same feature that already exists, perhaps introducing new bugs.

![](/assets/2019-01-18/top.jpg)

<!--more-->

There are lots of good reasons to remove technical debt, or even refuse to accept it at all.

Quick solutions can often:
* have serious flaws, most often for edge cases.
* take a lot of manual setup effort from developers.
* be inflexible to modify.
* not be optimised.

The first & last point seem the most pressing, yet they are generally the _least_ problematic. At least from a dev's perspective. That's because if something has serious flaws you'll be forced to eventually deal with it anyway, being forced to deal with tech debt is a good thing. And for the last point, you should only optimise when you need to anyway.

So, for me, it's the two middle ones that are the worst. They make developing harder and less fun, they make the final product harder to make or improve. If something is kinda hard to improve, you kinda won't want to improve it. Worst of all because in the end the functionality _seems_ ok, why should a product owner ever change it? Because of this, this kind of tech debt is the most risky to take on.

## Tech Debt in Robo Instructus
I don't need to worry about my product owner too much, because he's me. So let's take a look at some technical debt I've been paying off this week. Robo Instructus code examples.

<p align="center">
  <img align="center" src="/assets/2019-01-18/code-sample.png" />
</p>

The game has lots of code samples in it, because it needs to teach players the coding language of the game. These are just literally screenshots of the game with a border added in gimp. Just like the image above they are not text, just a picture of text. Which is kind of fine, they look the same and images are very easy to render.

### Flaws: Scalability
The biggest issue with them is they won't scale well. What about players with 4K+ screens? Try ctrl-scrolling into this web page, you'll see this sentence looking sharp as ever. But the image above is either the same size, ie too small, or has blurred at the larger size. That's because text glyphs are scalable, PNG images not so much.

So supporting high resolutions is already one reason to move away from images. Good resolution support is something that is actually pretty bad generally in games. Lots of devs hand wave it away and just make 1080p _(or whatever is popular)_ look fine. However, I want Robo Instructus to have excellent support for different resolutions. If you have an 8K screen the game should just _look better_, or at least as good.

### Effort & inflexibility
As I mentioned earlier, actual flaws are good technical debt. They stick in the mind and cannot be avoided by higher ups. The worst thing about the code samples though are the effort they take to create. Most of them show how the execution moves through the code, just like how you see it in game on the actual solutions.

This means I need to create frames for an animation to show the execution.

<p align="center">
  <img align="center" src="/assets/2019-01-18/loop-anim.gif" />
</p>

So now I have to take screenshots for each phase of the code execution, crop and wrap each of them in a border. I then need to implement animation rendering of the images. I have to do this for each sample & for any new sample. Even worse, if I think "this sample could be clearer if it used ***robo_left()*** instead of ***example_1()***", it's annoying to change as I need to re-do all the steps to get there.

Take a look at the above image again. The first comment has 1 space before it, the second has 2. Wrong! But I'm not going to take 9 screenshots, crop and border them just to fix that.

## Time to pay
For me it's time to pay this debt off. That means implementing code samples as proper text rendering with live code running & highlighting just like the real level code. It will scale to high resolutions. It will be easy to edit and create new samples. It will stay in line with improvements to the code renderer and colour changes. On the downside it takes effort to develop better solutions!

Let's take a look at new versus old, now I've mostly completed the implementation. The new version with scalable text rendering with actual code running underneath is placed above the old image animation. You'll need to watch this in high quality to see the difference.

<div class="video-wrap">
  <iframe width="850" height="478"
    src="https://www.youtube-nocookie.com/embed/HvbirnLTAqQ"
    frameborder="0"
    allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>

After all that, at 1080p it's going to look pretty much the same. But I hope you can now understand how I'm very glad to be rid of this debt.
