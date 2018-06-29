---
preface: robo-2
title: Summarizing The Summary & Alpha-1.13
---
This week I've been working on lots of under-the-hood improvements to Robo Instructus from the point of view of the later "probo" levels. Despite the alpha-1 part of the game being mostly unchanged I've made a new release ***alpha-1.13*** containing all the fundamental engine changes that have taken place in the last few months. Let's take a look at a small UI change that _will_ be visible in the release.

![](/assets/2018-06-29/simple-summary.jpg)

### Available Function Summary
Robo Instructus already has a summary for the available API to players. It's a blue bar at the top of the code that tells you what functions your robot can use. Each function takes a line along with a brief description to remind you what it does.

This is really useful to have, although with a load of functions it can start to get a bit big. Previously I just added a button to toggle it, so you could hide it completely and called it a day. However, since I've been working on the probe levels things have got worse. The probe adds another code panel beneath the robot one, with it's own blue bar of available functions.

![](/assets/2018-06-29/probe-summary.jpg)

The summary is starting to take up a large proportion of the screen height now there are are two. But I found I didn't really want to hide them totally, as they are really useful to have around. So instead I thought actually players are unlikely to be interested in the description of ***robo_left()*** after a few levels, they'll know what it does. After a while you'll just be interested in what you have available and you'll _hopefully_ be past wondering what the function does.

### Available Summary Compression
So I figured compress the available functions that the player has already used a few times before into a single line, and just show novel functions along with a description. Best of both worlds.

![](/assets/2018-06-29/compressed-mixed.jpg "Squished into a single line, but each is still a link to it's full documentation.")

This seems to work well enough that I got rid of the button to remove the summary totally, now it should never become too big and get in the way of a players mess of code.

### A Simple Change?
I thought so, but I hit a bug in my text library that cause the line-breaks to not work properly with all the functions in one line. I had to roll up my sleeves _(not literal, it's summer)_ and re-write _gfx-glyph's_ layout code. A couple of days later the issue is fixed, and the layout code runs over twice the speed as a nice bonus for my efforts.

### Alpha-1.13
It's been a while since releases and that's expected as I've been working on post-alpha features of the game. But so much of the core game code has shifted that it's useful to have an up-to-date build available to the testing group. Along with the spattering of new stuff is a whole shift in the engine and a huge number of dependency updates from around the rust gamedev community. Including my own [gfx-glyph](https://github.com/alexheretic/gfx-glyph/releases/tag/0.12.0) crate the latest version of which also released today.

So ***alpha-1.13*** should just be a little leaner, faster & better than previous releases, let me know otherwise test people!
