---
preface: robo
title: Putting The "Robo" In Robo Instructus
---

My work continues on feedback gatherin' playable alphin' code for this game of puzzlin' robot engineerin'.
Ahem. This week I've made a nicely visual step by replacing our panda protagonist with an actual robot character who can even face more than one direction. I've also added animation effects for each API call.
These new assets are *still* placeholder pixel art, but they're important as a information relay to players.

<p align="center">
  <img align="center" src="/assets/2017-08-18/robot.gif" alt="Come on, at least he looks like a robot now" />
</p>

It's a robot! A robot rendered in authentic *Alex Butler* 32x36 pixel art. Say hello to our new placeholder hero. I'm aiming for *cuteness from primitivism* with my pixel art. So hopefully that's what you're getting from it, rather than that it's just *bad*.
The important upgrade, though, is that he can face all 6 directions currently required by the triangles levels. This matters when you're trying to reason out where a wayward ***robo_left()*** will send the little man.

Lets see the difference along with the API animation for scanning etc. *My solution is hidden in the video to avoid spoiling the levels.*

<video src="/assets/2017-08-18/new-animations.mp4" controls loop></video>

The effects for the duration of ***robo_detect_adjacent()*** & ***robo_scan()*** make the biggest improvement to the legibility of whats actually happening. The robot actually looking like a robot and facing the correct direction is a big plus too.

I am aware the robot movement animation aren't very fluid, in my mind this can wait until the pre-release art overhaul. So I hope you can bear the jankiness for the time being, and in the alpha builds.

In summary; more features nailed down for the first playable alpha, and I'll continue with that next week. Check back then for more progress. I'm getting there.
