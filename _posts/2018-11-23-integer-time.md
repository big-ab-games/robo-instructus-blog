---
preface: robo-2
excerpt_separator: <!--more-->
---
In Robo Instructus player's solutions are timed to show off faster solutions. The timing is precise & deterministic to ensure a given solution always gets the same time on any system. This week I've made some changes to help clarify what impacts the time, from now on time is an integer.

![](/assets/2018-11-23/top.jpg "Much more discrete wouldn't you say?")

<!--more-->
Until now time had been shown as a decimal, which is normally pretty appropriate, but I've never been happy with it in Robo Instructus for a couple of reasons. Firstly it makes the time _feel_ imprecise like it was being measured on a stop watch. Under the hood each function always took an exact integer time, this was converted into the decimal time for display. So it always was accurate & deterministic, it just maybe didn't look it as much.

Secondly, in the game you'll be using & learning a bespoke language, an integer only language. So it seems appropriate that time would be measured as an integer too. This means in future I could support a ***sleep(time)*** function that waits an amount of time. With integer time this ties in with the function runtime and everything gels much more nicely.

![](/assets/2018-11-23/ms.jpg "Functions with exact integer runtime")

So ***robo_left()*** runtime changes from **0.275** tu to **275** Mimas-seconds. I'm binning the "time-units" (tu) as it seemed to baffle pretty much everyone. Instead I've made up a new time unit called "Mimas-seconds" or **ms** for short. At slowest speed you get around a thousand of these every real world second, so you can see I had to make up a new unit to convey this concept.

In the top-left of the world view you can see live stats as your solution runs. You now see the time tick up 275 smoothly as the robot turns left, 450 when you move forward etc.

<video src="/assets/2018-11-23/live.mp4" controls></video>

## Progress update
Tom continues working on the art assets and Rich the music. I've also been working on the company messaging system that completes the story systems and will be able to show some of that soon.

I'm starting to feel the need for more test feedback now the game is falling into place. If you'd like to test Robo Instructus get in touch, I may also open up alpha sign-ups at [www.roboinstruct.us](https://www.roboinstruct.us) again for a bit too so look out for that.
