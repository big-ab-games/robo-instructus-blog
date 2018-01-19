---
preface: robo
---
Wow [last week's post](/2018/01/12/getting-badder.html) was pretty impenetrable huh? This time lets relax and have a quick look at some new level features coming in the full Robo Instructus release.

### Launcher tiles
The [2018 plan](/2018/01/05/2018-plans.html) kicks off with adding enough new levels to last a player a game's worth of puzzlin'. This means new trials to deal with and new tools to help deal with them. In alpha-1 they was just tiles & the absence of tiles, in the full release they'll be more!

The 'launcher' tiles throw robots about the levels. When a weight is on the tile it starts charging, if the weight (ie the robot) remains upon the tile for the short charging time it'll _launch_ the contents a set distance.

They work a bit like this, _with red colouring taking the place of proper art and a quick and dirty jump animation_:

<video src="/assets/2018-01-19/launcher.mp4" loop autoplay></video>

So now you can get launched about the level. Notice the charge time is long enough to be able to move onto and off from the tile, but not long enough to mess about. The tiles will have a unique _robo_scan()_ code and later you'll find tools to help figure out if the trip will end in untimely robo-death.

You may need special behaviour if you want to make sure to use the launcher and maybe even special-er if you want to make sure _not_ to. What if an unknown tile turns out to be a launcher... Should be fun times!
