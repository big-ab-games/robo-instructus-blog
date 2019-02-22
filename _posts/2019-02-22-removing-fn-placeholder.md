---
preface: robo-2
title: Goodbye Placeholder Robot
excerpt_separator: <!--more-->
---
Final tile artwork and robot animations have already arrived for Robo Instructus. So why do the unlock screens, seen when you uncover new functions, still show placeholder art? This week I fixed this issue, it took a while because I wanted to fix it "right".

![](/assets/2019-02-22/top.gif "Decoding post-process fx for generated images")

<!--more-->
When players unlock a new function it comes with a description and an image of the function in action. It's an important part of explaining what the new thing is & how you can use it. Important enough that I had placeholder versions of most of them.

Take for example ***robo_detect_adjacent()***, a function that provides info about the tiles surrounding the robot. The game had a placeholder image for this.

<p align="center">
  <img align="center" src="/assets/2019-02-22/placeholder-detect-adjacent.png" title="Detecting in alpha-1" />
</p>

This image appeared below the function description in the game. And it works in-game pretty much exactly how it works in this web page. It's an image, pre-baked and shoved onto the screen. I created it by taking a screenshot of the game sometime in 2018.

Actually even before the final artwork arrived this image was out of date. This function actually highlights the surrounding tiles when it runs. This image doesn't have that because when the screenshot was taken those highlights hadn't been implemented. That's because taking screenshots and processing them is something I would have to do, and re-do for any change to fx, tile artwork, robot artwork etc. It's somewhat time consuming and quite boring.

So when the new robot & tile artwork arrived I was still hesitant to take new screenshots and process them into new images. They'd still be _wrong_ because the function effects are still placeholder, so I'd definitely have to do them all again. So why bother doing them now?

On the other hand I need to be rid of this bloody placeholder! Is there a way to remove the placeholder while satisfying my own programmer laziness?

### Generated Images
There is always as way. The game made the screenshots to start with, so of course it can make them inside _itself_. If the game renders these images itself the artwork and fx will never go out of date because they'll have the same source as the game does.

So it seems right. But actually implementing it is another thing entirely. Getting the game's render logic to work in a new context required some rework. Getting the decode fx to work on a non-image needed some post-processing, ie rendering to an image then rendering that image with the decode effect.

<p align="center">
  <img align="center" src="/assets/2019-02-22/native-detect-adjacent.png" title="It'll be like this, but on the other hand exactly not this" />
</p>

So the next version of the game will have a ***robo_detect_adjacent()*** visualization as above. But also much better than above, which _is_ just an image I made for this blog. When the robot animation is added, when the fx are added and when tweaks are made to tile or robot; the game will simply render it all up to date & able to render as high quality as the rest of the game.

This means it's finally time to say goodbye to my long serving placeholder robot. Buh-bye!

<p align="center">
  <img align="center" src="/assets/2019-02-22/bye-robot.png" title="Pull yourself together mate, placeholder panda was cuter anyway" />
</p>
