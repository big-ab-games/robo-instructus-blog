---
preface: robo-2
title: Dark Stages & The Fight Against Cheese
excerpt_separator: <!--more-->
---
Today the [final update](https://github.com/big-ab-games/robo-instructus/releases/tag/beta-3.3) to the beta is coming out before this phase ends. The beta phase is ending to make way for the full game's release. Robo Instructus will be released on the **16th July 2019** on [Steam](https://store.steampowered.com/app/1032170) & [itch.io](https://bigabgames.itch.io/robo-instructus). As you would expect with the game so close to release, I haven't been working on new features and instead have been polishing & optimizing the game.

<video src="/assets/2019-06-21/dark.mp4" loop autoplay muted></video>
<!--more-->
Psych! I've actually developed a major new feature called _Dark Stages_. All in the name of the fight against cheese.

### What is cheese?
Firstly a bit of background. Each level in Robo Instructus is made up of multiple stages, each a variant of the same general problem. The game has multiple stages to require a general solution that can solve all of them. If you only had to solve a single stage it would be fairly easy to "brute force" a hardcoded solution with just ***robo_forward()*** & ***robo_left()***.

But how "general" does the solution have to be? If you can figure out exactly which of the stages the robot is currently on you can switch to an optimized hardcoded version that solves that stage in a dumb but efficient way. I'll call this method "cheesing".

Cheesing a solution, _instead_ of solving it generally, isn't really in the spirit of the game. But in the earlier levels it's actually quite a bit harder to cheese a level than it is to solve it generally. When this is true I'm cool with cheesing,and this is also why I hadn't really addressed it directly.

As the challenge offered by levels increases so does the difficulty in writing the "proper" solution. The relative difficulty of a cheese solution can make it start to look more attractive. Ultimately this is a problem because writing cheesy solutions in later levels just isn't fun. Adding salt to the wound, cheesy solutions will probably score better than general ones.

### Dark Stages
I want to encourage proper general solutions to the levels. With that in mind I've added _Dark Stages_ to all the mid & late game levels. These are extra stages very similar to the others, but their features are hidden. When you can't see or analyse the layout of a level they become very difficult to cheese, yet a general solution to the visible levels will solve them without issue.

So if you're already coding general solutions the new stages won't hinder you at all. On the other hand let's take a look at a cheesy solution to _Into The Unknown_, which is the first level with dark stages.
<video src="/assets/2019-06-21/cheese.mp4" loop autoplay muted controls></video>

You can write this sort of solution by appending stuff to a naive approach each stage, it's pretty ugly but it will work. However, when you get to the dark stages it now becomes impossible to "see" how to modify it to pass the extra stages. This should encourage players to seek an algorithm that will solve all levels of the ilk of the visible stages.

So the dark stages are a powerful weapon against the cheesy solutions which damage the fun of the game. They do have a problem though. The dark stages are very similar, but they obviously aren't _exactly_ the same. If a player wrote a general purpose algorithm which just happens to have a flaw only uncovered in a dark stage it creates a quite unsatisfying game experience, the dark stages are necessarily difficult to debug.

To ease this issue while you cannot get a score without solving all stages, including dark ones, if you complete all the visible stages you _will_ be able to progress to later levels. This means if you can't debug your algorithm that fails in the darkness, you can at least still continue with the game. This detail should prevent too much frustration when the dark stages "go bad".


### Release
Oh yeah the game is releasing soon too. 16th July. Hopefully we'll start seeing reviews and stuff about the game in the next month. Please wishlist the game on Steam to help it's visibility there.

**Beta-3.3** brings a bunch of performance optimizations and improvements to things like window resizing too. So I am polishing & removing the game's hard edges. I'll continue to do this as the release approaches.
