---
preface: robo-2
title: DPI Transparency & Scaling
excerpt_separator: <!--more-->
---
DPI/PPI (dots/pixels per inch) is the measure of how many pixels your monitor crams into it's rectangle of illumination. In general DPI is handled quite poorly on the desktop & in games. Desktop software seems to think that more DPI just means being able to have _even more desktop shortcut icons_. In games resolution is often locked and stretched over your monitor like a texture over Max Payne's face. This isn't really what pixel density should be about though.

We have been seriously mis-sold PPI.

![](/assets/2019-01-25/top.jpg "Everything should scale nicely, though this is just an jpg so it won't...but the game will!")

<!--more-->

### High DPI should mean better fidelity
Take a look at a smartphone from the last decade they have massively higher pixel density than desktop screens, yet somehow the text is still readable and the icons are bigger than atoms. That's because they're designed to handle DPI properly as a way to achieve higher fidelity.

So as I have opinions on this I've naturally baked them into Robo Instructus. The game is _"DPI transparent"_, I mean by that that the game will try to render at the same proportions whatever DPI you throw at it. So a 4k, 1440p and 1080p 27" screen will all have the same look with higher resolutions giving better quality.

Unlike last weeks look at [some technical debt](/2019/01/18/paying-off-tech-debt.html), DPI transparency was a goal throughout development of Robo Instructus. Pretty much everything in the game scales based on resolution, and is scalable like text or high quality enough images that they can be scaled up fairly well.

### Custom scaling
So this style of sizing means people with 4k, 8k and 1080p can all play the game as best as their monitors allow, and that's great. One problem with the game currently is that it treats a 4k laptop 17" screen the same as a 4k 50" TV. Quality isn't the issue now, it's just that the text is too bloody small.

One side effect of scaling the entire game to handle any DPI is that it's quite feasible to introduce custom scaling on top of that. So I've been working on exactly that this week. The game will have an option to set a scaling value to grow/shrink the UI to whatever suits the player best.

So maybe on a huge desktop monitor you might want smaller scaling.

![](/assets/2019-01-25/720p-scale-0.8.jpg "Scale 0.8x")

While back on the 17" laptop a larger UI may be appreciated.

![](/assets/2019-01-25/720p-scale-1.5.jpg "Scale 1.5x")

This scaling is now working well in the game in a decent range that should serve pretty much everyone. I'm going to do some work to try and guess a good initial scaling value from the monitor & OS DPI settings & size. But this will also be selectable by players on a sliding scale.

### World scaling
One exception to the above is a hangover from the placeholder pixel art days; the game world don't scale in a DPI transparent way. However, with proper high quality art assets there's no longer a reason for this. Bloody technical debt again, will fix!

##### Comment on [twitter](https://twitter.com/bigabgames/status/1088824628045406208) | [facebook](https://www.facebook.com/bigabgames/posts/2267909346629773)
