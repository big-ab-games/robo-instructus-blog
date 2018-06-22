---
preface: robo-2
title: Harnessing The Probe
---

[Last week](/2018/06/15/probo-instructus.html) I was detailing some of the difficulties of implementing Robo Instructus' latter concurrency puzzles. Today I'll take you through what this means from a player point of view. How do you use this probe to actually solve some levels?

![](/assets/2018-06-22/top.jpg "Take good care of your probe")

On these final levels you have both the robot and the probe. However, the objective remains the same. That is to get the robot to the level exit. The probe doesn't need to be at the exit, she's just here to help!

The probe will take on some of the functionality the robot previously had and adds the ability to travel over gaps. Together they're more powerful than the robot ever was, but as in any relationship the key to success is communication.

### Communication
The robot & the probe can talk using two new functions.
```python
# transmits data on a subject
transmit(subject)
# consumes & returns the oldest subject data value, or -20000 if none exists
receive(subject, data)
```
With these two bad boys players can setup any communication channels they might need to pass information between the probe and robot. It's a simple push & listen type messaging system, an important point is the functions do **not** block. That is, a ***receive(123)*** call will not wait for a message to appear it either returns a message or ***-20000*** the _"no message"_ error code.

I'll show you an example, which will be similar to the first probe & robot level in the game. Take the following 2 variants and imagine we need to get the robot to the top tile of both with a single program.

![](/assets/2018-06-22/level.jpg)

Pretty simple. But now cosider that the robot has only ***robo_left()***, ***robo_forward()*** regular functions. This means the robot simply cannot solve both variants. The robot has no _eyes_ to see where to go.

The probe is here though, she can move about too and has ***probo_scan()***. So if we can get the probe to go and scan where the robot can't the probe will become the robot's eyes.

Because it's simple I'll take you through it in detail.
#### Probe
- Go to the first tile that could be missing, lets say the one on the right.
- Scan it, and send the scan result to the robot

  ![](/assets/2018-06-22/probe-plan.jpg)

#### Robot
- Go forward one _(as it's always safe in front)_
- Wait until a message can be received
- Use it do decide whether to go around left or right

  ![](/assets/2018-06-22/robot-plan.jpg)

Shoving that in code we get:
<video src="/assets/2018-06-22/plan-in-motion.mp4" controls></video>

A nice example of working together! Notice how the programs run without blocking each other, though the robot explicitly waits for a message.

Of course, this could have been solved with a single ***robo_scan()*** if it were available. But as players progress they'll have to more fiendish puzzles that could never have been tackled single robot logic.
