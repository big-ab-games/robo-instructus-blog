---
preface: robo-2
---

Work continues on the final puzzles of Robo Instructus. For today let's take a look at a level coming after the alpha-1 levels, one that's deceptively simple. In [asking for a little more](/2018/02/09/asking-for-a-little-more.html) I introduced some new tools available in later portions of the game, in general you build up tools and have to use them together. However, in the level I want to show today you'll be running blind without the old guard of ***robo_scan()*** & ***robo_detect_adjacent()***.

![](/assets/2018-04-13/blind-screen.png "Moving without "seeing"?")

One of the impacts of not having ***robo_scan()*** available is even if your robot is standing next to an exit tile, you can't actually tell. If a tile is unknown, or missing you can't directly tell. But perhaps you can navigate the level regardless by just using what you have?

<video src="/assets/2018-04-13/blind.mp4" loop controls></video>

Of course there **is** a way to successfully route safely through the level, even without your ***robo_scan()*** eyes. Doing the utmost with what little you have is what Robo Instructus is all about. Then later your eyes will return, you'll need them _and_ what you learned in the dark.

And this is all before you need to meddle with actual concurrency, the current area I am developing right now.
