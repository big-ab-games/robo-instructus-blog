---
preface: robo-2
---
After last weeks ***alpha-1.13*** build I started thinking about how designs for the late game may help the early game. In particular the current ramp of levels runs straight into a brick wall of difficulty, the deceptively tough "ring" level. I've been wondering how I can improve the early learning curve. So I'm adding a new concept that will appear early, _usables_.

![](/assets/2018-07-06/usable-level.png "Where's the bloody exit?")

Usable tiles are a new variant that return information when using a new function ***robo_use()***. The first one I designed returns the location id of a safe tile that scans as unknown. So in the picture above the safe tile is in fact the exit of the level.

Using stuff in the levels is a pretty intuitive idea for gamers, and also allows me a lot of freedom in puzzle design with a single new function. Later on we'll find different usable tiles that must be handled in different ways.

<p align="center">
  <img align="center" src="/assets/2018-07-06/usable-tile.png" title="Placeholder blue for now..." />
</p>

On one hand this just introduces yet another concept to the early game. But the payback is the chance to practice puzzle solving skills on more intermediate levels without the difficulty ramping up so quickly. I've received feedback that this is a problem with the current game builds.

In particular the "ring" level that so many get stuck on requires you to use the location id functions in a novel and not immediately obvious way. Even worse this is the first time you _ever_ use location functions so can be a bit much. The first new usable puzzles will come before then and ease you in. They too require saving a location in a ***var*** for later comparison, but are much more direct about what you need to do.

Let's see one in action.

<video src="/assets/2018-07-06/usables.mp4" controls></video>

This also gets the player traversing unknown-tiles a little earlier than the meatier puzzle of ***robo_detect_adjacent()***. This concept isn't just for early game though, usable tiles are part of harder later levels too. Look out for new puzzles coming to the alpha builds soon.
