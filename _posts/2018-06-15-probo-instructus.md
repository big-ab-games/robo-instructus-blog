---
preface: robo-2
title: Probo Instructus - Deterministic Concurrency
---

A little while back I wrote about the [puzzling concurrency featured in the final Robo Instructus arc of levels](/2018/03/09/robo-concurrency.html). A major difficulty of letting users code 2 things that run disconnected from each other is getting the results to be deterministic. Determinism means that a solution to a level will always run the same way and produce the same score, and this is important for a puzzle game that's going to berate you for not doing as well as your mates!

![](/assets/2018-06-15/robo-probo.jpg "A perfect match of robot & probe")

First what's all this concurrency lark about? The idea is in the final 3rd of the game you'll be a accomplished robo-instructing elite. In the puzzle tradition it'll be time to make you frown anew, but in a good way! You'll go from controlling just one little robot, to two things at once. Each is programmable and runs simultaneously, whats more you'll need to use both to achieve your goals.

Introducing **the probe**. This little code-able flying machine is fast, loaded with useful functionality and **can't fall off the edge of the level**. _I've mocked it up with some more pixel art in the same vein as my current placeholder art_.

<p align="center">
  <img align="center" src="/assets/2018-06-15/probo.png" title="Hello Probo!" />
</p>

You'll need to write separate code for the probe and the robot. With some simple communication primitives provided, running together they may solve the puzzle. I'll perhaps talk more about this later, before that though let's go under the hood: What's all this determinism guff?

<video src="/assets/2018-06-15/running.mp4" loop controls></video>

It may not seem like a hard problem. We have 2 processes running now, so what? Well we basically want to ensure that a given solution always gets the same score after multiple runs, or running on a different machine.

### Time units (tu) score
The first score in the game is the **time units** the solution took to complete. This is the sum of how long all ***robo_**** functions take to complete. Notice this doesn't include any of the time it takes for the program to get around to calling these functions.

In the game all pure code is modelled to compute instantaneously, so no matter how complex it is it won't affect your **tu** score. Of course, in reality this is not the case. The speed of the in-game code interpreter is dependant on the machine running it and the selected code-speed.

This is not a big deal for one robot, just count all the ***robo_**** function calls. But with 2 guys talking to each other this is not trivial. If the probe sends a message to the robot will it arrive before the robot calls ***robo_left()*** or afterwards? Will that be the same on a really slow/fast machine?

### Solution & Run score
Also problematic are the code scores. The **run** score is an efficiency rating, _maybe I should actually call it that_. It's a count of every executed code operation. So the more messing about in code the higher & worse the score, even if it doesn't affect the **tu** score.

If you have 2 processes running counting operations, how can will the sum be consistent?

### World deterministic lock-step
To address this there is a synchronisation occurring in the game world. Remember the game world models code computations as being instant. This means to enforce this model we, for example, make the ***robo_left()*** "wait" until a ***probo_forward()*** has been called before it can progress. How much the world time can progress is the minimum cost of the synchronised function calls. This means some calls have to "halt" halfway through until another, e.g. ***probo_left()***, call comes in.

<video src="/assets/2018-06-15/lock-step.mp4" loop controls></video>

This is a sort of advanced version of a roguelike's simultaneous turn, but every function has a different "turn" duration e.g. the probe moves much faster than the robot.

The 2 running processes are spinning independently but when they call out into the world each moving part's functions wait for an _agreement_ that a certain time has passed. This mechanism allows consistent behaviour of a pair of programs running, as far as the player is concerned, totally concurrently.

The reality is a _little_ more complex as we have issues like environmental delays (launcher tiles) and variable cost functions. But these are all surmountable or already surmounted.

If players can _actually get past the first two thirds_ of Robo Instructus they're in for a delightfully concurrent new puzzle-cake to bite into. Bon appetit!

##### Comment on [reddit](https://www.reddit.com/r/rust_gamedev/comments/8rb5mh/robo_instructus_coop_for_one_deterministic/) | [twitter](https://twitter.com/alexbutlergames/status/1007622995177811968) | [facebook](https://www.facebook.com/alexbutlergames/posts/1921291631291548)
