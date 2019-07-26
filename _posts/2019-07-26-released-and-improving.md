---
preface: robo-2
title: Released But Still Getting Better
excerpt_separator: <!--more-->
---
On the 16th July Robo Instructus was released on [Steam](https://store.steampowered.com/app/1032170) & [itch.io](https://bigabgames.itch.io/robo-instructus) for Linux & Windows. But development is not over just yet. Today I'll be releasing Robo Instructus 1.2 ([release notes](https://github.com/big-ab-games/robo-instructus/releases/tag/1.2)).

<p align="center">
  <img align="center" src="/assets/2019-07-26/best-comparison-time.jpg" />
</p>
<!--more-->

## Having a peek
One cool thing about releasing a game in 2019, even a small one, is that you'll be able to find videos of people playing it. This is really interesting & valuable to me as I haven't been able to observe as much playtesting as I'd have liked over the course of development. So I've been having a peek at the youtube & twitch videos of the game.

Overall the game seems to be working pretty much as expected. I'm fairly happy with the difficulty curve through the crucial first act of the game. Of course this is a difficult game, even more so if you haven't programmed before. But the determined _are_ succeeding and it looks like the game is mostly communicating it's concepts successfully. Of coures there were also some areas that I wanted to improve.

## You didn't read it!
When you unlock functions & primer sections throughout the game, they can withstand being ignored. I expect some players to not read things up front in detail, instead return to a concept then they struggle. So the code reference and message archive store all unlocked information. There's also a company inbox to re-read those messages.

One thing you can't see again though is the overlay tutorial messages. I think mostly this is ok, but in at least one case this hasn't been ideal.

![](/assets/2019-07-26/change-speed.jpg)

Knowing that you can change the game speed is really important. _Actually take note **Sins of a Solar Empire**, I played so many 100% slow speed games of you!_

In v1.0 if you ignore earlier tutorials you could never even see this important UI tutorial. In v1.1 I fixed this in 1.1 so that it will always appear in the 2nd level... But players _still_ missed it. So in the 1.2 this tutorial just won't disappear until you click it.

## Improving optimisation
Lots of players like optimising their scores and generally I'd say the scoring mechanism has gone over well. I wanted to make the feedback better for when you improve a solution and run it again. Currently it can be hard to know if the new solution was actually any better, you pretty much had to remember what it used to be.

So let's say you've just solved _Use Your Powers Wisely_ and you see a way to solve it faster. New in 1.2 when you run you're new and improved solution you'll see this.

![](https://user-images.githubusercontent.com/2331607/61949715-a12b2480-afa3-11e9-9d2d-734cde91a79e.gif "Getting faster on Use Your Powers Wisely")

As before your best scores are saved and shown in the graph. But now the game will remember your _previous_ best score before the latest run and tell you if you did better. It'll also show much more clearly if the new faster solution is a little worse than your best when it comes to _Solution_ & _Run_ sizes.

## Graph squashing
There's a bit of a flaw with the game's graphs that never mattered too much with the smaller alpha & beta communities. If someone gets a poor score it will be shown on the linear graphs with the rest, but if it's a **very** poor score (or very optimised in another area perhaps) it'll end up squashing the majority of the scores into the left of the graph.

It is interesting to see these extremely bad scores, but it also harms the ability for players to see how well they're doing compared to others. My solution is to filter out scores more than 2.5 standard deviations worse than the mean. But this can also be disabled if you want to see the outliers.

![](https://user-images.githubusercontent.com/2331607/61949239-0bdb6080-afa2-11e9-973c-7070471d555e.gif "Graph squashing on Use Your Powers Wisely")

## So how did the release go then?
You want to know if I'm a millionaire now my game's out huh? Well I'm as baffled writing this as I'm sure you are reading it, but the answer is **no**. The first week after release was a bit mixed, one one hand the game was on the front page of Steam for over 24 hours and this is a huge deal, on the other hand Robo Instructus has unfortunately been largely ignored by the mainstream press.

![](/assets/2019-07-26/ways-to-get-rich.jpg "Hmmm I don't see what I'm doing wrong...")

The game has got a bunch of sales, most strongly in USA, Russia & Germany. Then UK... _4th place UK come on? And after I came from you!_ There are people really playing my programming game and that's just amazing, even though I've had to cancel all my yacht orders.
