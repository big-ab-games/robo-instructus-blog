---
preface: robo-2
excerpt_separator: <!--more-->
---
The most difficult challenge in having people enjoy your game is getting them to play it at all. This battle is mostly fought outside the game itself by getting the word out. The next biggest is perhaps the first session after they start the game. The game must introduce itself and first impressions count.

![](/assets/2018-10-19/intro.jpg "Overlay tutorials as the game introduces itself")

<!--more-->

That first session of Robo Instructus has been my focus this week. When players load up the very first level they're going to be met with a strange scene. On one side, a frozen skeleton of metal backing a robot at the foot of a maze wrought of triangles. On the other, a dark rectangle with a couple of mysterious ***robo_forward()*** scrawls. Dotted around the screen are buttons and symbols that presumably will mean something.

Players may now be a little confused.

_What is this game and is it for me?_ _Did they leave it in dev-mode?_

Maybe it is! And <s>no</s> wait yes, sort of but now _you're_ the dev.<br/>...Come back!

I'd like to be there to answer these initial worries, to direct players to try the game out a little before making judgements. You type commands on the left there. Try typing a couple in. Now press play to run them. See? Now try to get the robot over there...

But I can't be there every time a new player plays the game, there is only one of me yet the game could sell to **dozens**. So I'd like my game to introduce itself.

## Overlay tutorials
My solution is to overlay hints in the early game to get players started.

<p align="center">
  <img align="center" src="/assets/2018-10-19/type-commands.gif" title="Type what you see" />
</p>

These are direct notes from me to the player, I found a font that helped make them resemble annotations I'd written on top of the game. At least in a parallel world where my handwriting was legible.

## Tooltips
Once you're introduced and able to play the game, you might start investigating the other buttons and symbols on the screen. Some of them I'll hide to avoid the complexity, but others will remain. It's generally expected for UIs to remind the user what buttons mean via tooltips, so I implemented these this week too.

<p align="center">
  <img align="center" src="/assets/2018-10-19/tooltip.jpg" title="Ah THATS what that does" />
</p>

Tooltips are low-glory features, but expected by players and indeed very useful. I've also added the hotkeys to the descriptions. Yes there are hotkeys for most things, soon players will be wizzing through the game like vim users, or at least vim users using nano.

See this in action and, if you please, contrast the following video with the one I [posted last week](/2018/10/12/early-game-discoveries.html).

<video src="/assets/2018-10-19/first-level.mp4" controls></video>

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/9pmm15/robo_instructus_introduce_yourself/) | [twitter](https://twitter.com/bigabgames/status/1053354033937821701) | [facebook](https://www.facebook.com/bigabgames/posts/2120318374722205)
