---
preface: robo-2
excerpt_separator: <!--more-->
---
Another week, another update. Today it's **beta-2.1** and hot news is Steam Achievements. 8 of them are coming to Robo Instructus and are now available for high flying beta testers to unlock. [Release notes](https://github.com/big-ab-games/robo-instructus/releases/tag/beta-2.1).

<p align="center">
  <img align="center"
    src="/assets/2019-05-17/done-arc-1.jpg"
    title="Into The Under" />
  <img align="center"
    src="https://user-images.githubusercontent.com/2331607/57933215-91f96d80-78b4-11e9-8fb6-15ad754f937a.jpg"
    title="Get The Gist" />
  <img align="center"
    src="https://user-images.githubusercontent.com/2331607/57933256-b05f6900-78b4-11e9-9969-10539a2311f3.jpg"
    title="Optimizer" />
  <img align="center"
    src="https://user-images.githubusercontent.com/2331607/57933320-e270cb00-78b4-11e9-8233-6c5773c6d553.jpg"
    title="Into The Dark" />
  <img align="center"
    src="https://user-images.githubusercontent.com/2331607/57933300-d1c05500-78b4-11e9-9a64-64a092915bac.jpg"
    title="Putting It All Together" />
  <img align="center"
    src="/assets/2019-05-17/cereal.jpg"
    title="Serial Optimizer" />
  <img align="center"
    src="/assets/2019-05-17/done-arc-3.jpg"
    title="Two Heads Are Better Than One" />
  <img align="center"
    src="/assets/2019-05-17/maze.jpg"
    title="Blind Mastery" />
</p>
<!--more-->
### Achievements
In getting steam achievements into the game I've had to integrate the Steam API libraries for the first time, not a trivial thing for a Rust game as it turned out. I've also created some icons and the fairly straightforward logic to activate them. But before all that, why do I even want achievements in Robo Instructus?

It's worth noting, and indeed everything I note normally is, that I'm not _too_ fond of how achievements are used in many games. As a player I find them mostly redundant and often just not very impressive. I really don't like playing the tutorial or first level of a game and seeing 7 achievements spring up before I even understand what I'm playing.

However, Robo Instructus is unlike a lot of other games in that it just isn't a very easy ride. Progressing through this game will be tough, so achievements will be well earned. Overall I'm keeping the count pretty low and want each to feel like a literal achievement.

From a dev's point of view achievements are in theory a pretty cheap way to generate a little word of mouth as people see their friends unlocking achievements they may become a little more interested in the game too. This little one man game of mine is really going to need all the word of mouth it can get, so this is an important reason in itself.

Actually if you consider the publicity side of it you can explain quite why so many games have tons of junk achievements. I think it's a line that can be walked, achievements don't _need_ to be bad right?

Let's take a look:
#### Get The Gist
![](https://user-images.githubusercontent.com/2331607/57933215-91f96d80-78b4-11e9-8fb6-15ad754f937a.jpg)

_Complete Testing Grounds._ This one is doable, _Testing Grounds_ is the 4th level and first where you have to design a simple algorithm and use the language a little bit. No problem, I believe in you!

#### Into The Under
![](/assets/2019-05-17/done-arc-1.jpg)

_Discover the underground facility & complete act 1._ This means doing every above ground level. The real game is underground so you need this achievement otherwise you can't say you've _really_ played Robo Instructus. You can do it!

#### The rest of them
<img align="center"
  src="https://user-images.githubusercontent.com/2331607/57933256-b05f6900-78b4-11e9-9969-10539a2311f3.jpg"
  title="Optimizer" />
<img align="center"
  src="https://user-images.githubusercontent.com/2331607/57933320-e270cb00-78b4-11e9-8233-6c5773c6d553.jpg"
  title="Into The Dark" />
<img align="center"
  src="https://user-images.githubusercontent.com/2331607/57933300-d1c05500-78b4-11e9-9a64-64a092915bac.jpg"
  title="Putting It All Together" />
<img align="center"
  src="/assets/2019-05-17/cereal.jpg"
  title="Serial Optimizer" />
<img align="center"
  src="/assets/2019-05-17/done-arc-3.jpg"
  title="Two Heads Are Better Than One" />
<img align="center"
  src="/assets/2019-05-17/maze.jpg"
  title="Blind Mastery" />

The rest of them are hard.

### Steam API integration for rust games
As you may know Robo Instructus is written in Rust. Rust is an amazing language that only really has 2 downsides; compile times and not being ancient. The latter means that support for stuff just isn't always there. This time it's the Steam API, a C++ library for doing steamy things like achievements & tons more.

There is a project for wrapping the steam API in a rust layer [steamworks-rs](https://github.com/Thinkofname/steamworks-rs). But this didn't include the achievement bits, and didn't compile for me. So what do you do in these situations? Submit some pull requests! I did just that and after [#7](https://github.com/Thinkofname/steamworks-rs/pull/7) & [#8](https://github.com/Thinkofname/steamworks-rs/pull/8) the crate compiles and provides Steam achievement functionality.

This is the first time I've had to deal with bindings to C/C++ and as I haven't done projects in these languages before it's something I generally shy away from. Thankfully I only needed to tweak the bindings generation and I found the Steam API docs to be pretty good. Hopefully my efforts will make it easier for the next rusty guy to add achievements to their game, it's nice to feel helpful.

### Release plans
The Q3 release of the game is looming, which will mean the end of the beta. So beta testers; start unlocking those achievements.

##### Comment on [twitter](https://twitter.com/bigabgames/status/1129425315917422592) | [facebook](https://www.facebook.com/bigabgames/posts/2445288992225140)
