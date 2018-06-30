---
preface: robo
---

Work continues on improving the alpha version of Robo Instructus. The feedback I receive allows me to focus my efforts on the areas that matter the most to the alpha players. With *alpha-1.2* out today the early game experience and game system usability are both starting to improve.

![](/assets/2017-10-20/click-hint.png "Early game next-level button hint")

### Early game
The above image shows one small addition to help people the first time they fire up the game, just a piece of text appearing when you finish the level. It points out the next-level button. Any unfamiliar UI is bound to be a little confusing at first. That confusion makes you less likely to bother progressing, so I want to tackle this by making that crucial early experience at least make sense.

This game has a steep learning curve; learning a programming language. While really this isn't as scary as it may sound, it still represents an amount of dedication games don't normally require of players these days.

### You must gather your knowledge
The nice thing about logical languages is there are many ways to write a solution to a given problem. This is normally great, however early in the game this means you'll actually be able to get past levels without bothering to learn what the tutorials are telling you. I'd be ok with that too, if it works *it works*.
Unfortunately if you don't learn all of your basic tools you're going to have a lot of trouble later on.

To combat this in *alpha-1.2* some early levels can have *requirements*. That means as always you're free to solve them as you wish, but if you don't a tool **at all** that is really going to be worth knowing you won't be allowed to proceed until you do. You only have to solve the level once using the tool, after that you can solve it however you like.

Here's how it works on the '**loop**' introducing 2nd level.

<video src="/assets/2017-10-20/use-loop.mp4" controls loop autoplay></video>

This level just needs repeated commands to complete, using a **loop** is a nice fit so maybe give it a try?
In a lot of cases I think players won't ever see this message as they'll just be interested to try out the new tool anyway.

I'm keen to be a light touch with these sort of things and currently only two levels have such requirements.

### Mouse click & select
You may also have spotted selection using the mouse in that video. Yep you can click on and select code using the mouse now. This is an expected usability feature of any text editor really. It also comes with a load of nice extras like stopping the current run by clicking on the code, immediately entering edit mode. This should mostly be intuitive and make the game a little more fluent.

### Debugging
Once you're into the game you are going to spend time trying to figure out why your code doesn't work properly. This is what being an engineer is all about! This week the game has received some nice additions like stepping forward to the next code section using the *left arrow* key & the ability to run your solution on any of the level's variants first (very useful when your code doesn't work on just the last one!).

### Filling tutorial gaps
More tutorial pages have appeared and some have moved around. This is because I'm trying to put useful info in front of players when they need it, but not too much at once. It's a balancing act, and I'd appreciate help in optimising the tutorial experience.

### Saving progress
In Robo Instructus your progress is automatically saved as soon as you change or do anything. This week I've moved the save data to the correct place on the file system, which is platform specific.

The data I need to store changes as I add new features, which means a newer game version's saves aren't the same as the old. I've implemented a migration process to automatically convert older formats into valid up-to-date formats. This way I can handle the changes of the alpha without losing people's solutions and progress. It'll naturally allow me to continue to improve the game at any stage and retain progress.

Because of the above in future you'll be able to download the alpha, unpack it anywhere and your progress will be restored & available to the new version.

### Incoming
I still have many issues raised so far to work through improving the game. Next week should bring an even better alpha.

*If you fancy being a part of the alpha testing get into contact with me using one of the methods on the [front page](/).*

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/77nd2q/robo_instructus_you_must_gather_your_knowledge/) | [twitter](https://twitter.com/bigabgames/status/921418810321723392) | [facebook](https://www.facebook.com/bigabgames/posts/1631858330234881)
