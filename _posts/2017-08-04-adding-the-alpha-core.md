---
title: Adding The Alpha's Core
preface: robo
---
As the supernova remnant of my coding prowess relentlessly pulls in feature-planetoids on it's unstoppable path to 'playable alpha' girth; this week sees a UI for navigation within & between puzzles, separated APIs per puzzle and automatic progress saving.

In previous updates we've only seen a single level. KABOOM now we can view multiple level variants, and remember these are the guys that must be solved by the same piece of code.
Each puzzle can have a distinct set of API calls available. In this way complexity can be introduced gradually with new tiles and tools.

![](/assets/2017-08-04/screen-1.jpg)

### Per puzzle API
In the top left we have some documentation for the API calls we can make on these levels. I still aim to improve this section, I'm planning a tutorial for each of these functions so it is clear how these work when the first appear. This section should link to the tutorials, but right now its just some lovely code comments.

### Level variant selection pips
Below the level we have some dots/pips these map to the four level variants our solution will have to deal with. The larger pip is the level we're currently viewing. Clicking on these pips will allow viewing any level in the set.

### Previous/next arrows
To the left and right of the pips arrows allow navigation to the previous and next collection of levels respectively. The *next* button becomes unlocked when you have solved the current level.

### Saving progress
Along with these additions your solutions are saved, as you type them, and attached to a particular puzzle. There is more to do here managing multiple versions of a solution, having different play through saves etc. But, as it stands it's viable for the playable alpha.

Let's see it work in motion *(fullscreen the videos if you'd like to read the text)*. Please keep in mind that currently all the art assets, puzzle designs and APIs are placeholders.

<video src="/assets/2017-08-04/vid-1.mp4" controls></video>

So we solved the first level, *for babies*, and we can see hard-coded *robo_forward / robo_left* nonsense isn't going to cut it on the next one.

We need to use the newly available `robo_scan()` to solve these. So we use the simple 'go where it's safe' algorithm we've seen before.

<video src="/assets/2017-08-04/vid-2.mp4" controls></video>

Nice. Notice how I can call my function *is_safe* both like `is_safe(robo_scan())` or like `robo_scan().is_safe()` this is true of all functions in badder (the in-game language programming language). You'll also notice in the next level simply running *robo_scan* isn't going to be enough, but we have a new tool. Can you solve it in your head already?

Hold that thought for when you get your very own coding fingers on a build of the alpha.

The game is starting to appear a little more every week. Indeed, the core of the alpha is now in place. A player can actually play through all levels!

Of course, there remains much to do. I need to add nice error reporting, API & badder language tutorials, sand the edges off my font/code rendering, show a success screen & solutions stats, finalise my level & API design and add improved (though still placeholder) animations.

So check back again next week for more progress on those, and hit me with any questions on reddit/facebook/twitter.
