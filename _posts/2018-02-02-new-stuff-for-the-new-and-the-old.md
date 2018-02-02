---
preface: robo
---

Working towards completing the puzzle content I'm busy designing and implementing new levels and puzzle mechanics. A lot of the new stuff I'm a bit hesitant to talk about, but I've also made some improvements to alpha-1. In particular a new level!

![](/assets/2018-02-02/robo-detect-adjacent-intro-level.png "New level available in alpha-1.10")

As I was designing a new function coming in the full game I created a level and stripped down the availability of other tools. So you can really just move about and use this one new tool. I found it's a nice way of introducing a tool because it forces you to think about how it works in isolation.

### News for the olds
This made me wonder if this technique would help in learning ***robo_detect_adjacent()*** from alpha-1. That's when the game really begins, the first proper puzzle, but I think people are experiencing quite a spike in difficulty at that point.

To help with that I released **alpha-1.10** today, bringing a new level that removes location & scanning. You really just have ***robo_left()***, ***robo_forward()*** & a first go at ***robo_detect_adjacent()***. If you got stuck on the previous alpha's give this one a go and tell me what you think!

That's not all, my quest to improve the tutorials never ends. New for this level, I actually explain ***while*** and ***for*** looping.

![](/assets/2018-02-02/loops-iii.png "`for` a `while` this was not actually explained")

I've re-done part of the ***function*** tutorial to try and make it less abstractly based on plus-ing numbers and more on calling ***robo_x()*** functions that the player has been doing.

Finally **alpha-1.10** also brings new feature for the in-line debugger; highlighting 'constants' that you've named. They show up in brackets alongside the number when they're unique. Something like: `-999 (UNKNOWN)` instead of just `-999`.

![](/assets/2018-02-02/debug-consts.png "You do name your constants right?")

### News for the news
As mentioned I'm actively working on new stuff. But I'm keeping the build together in one, no weird branch stuff, and I'm planning yet more alpha-1 content. I'll tell you more later! _oooooooowwwwww._
