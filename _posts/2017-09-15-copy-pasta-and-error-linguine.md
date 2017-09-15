---
preface: robo
---

This week I have *delicious* improvements for all budding robot engineer commandos (that's you guys).

Ok so maybe *'Error Linguine'* isn't the best. *'Pizzerror'*? ... forget it. On with the devblog!

### Code Error Highlighting
![](/assets/2017-09-15/error-screen.png "That's not what it's called. TERRIBLE")

I've been made aware that many coders write code that won't compile, or will fail at runtime. I'm not sure why they do this, why not just write working code teh first time? *(I wrote 'teh' there on purpose for comic effect. Heh. This sentence is for those who would read that as me being both insufferable and having poor spelling, when only one of these is true)*.

Since I'm a man of the people I want to support this style of development and report simple helpful errors to get engineers back on their way. So lets have a look at this *error driven development* or *EDD* in action!

<video src="/assets/2017-09-15/error-highlighting.mp4" controls loop autoplay></video>

I actually have a lot of plans for errors in Robo Instructus. Partly because I have a fetishistic hankering for good errors messages, and believe them to be a mark of quality software, but also because I think in-game errors could be a chance to introduce a little humour to an annoying situation.
I was thinking on creating an AI character as the in-game *compiler*. More on that later.

For now I'll just try to make them useful for all the errors the alpha crops up. In fact, telemetry to gather such things will be an important addition when I open up the alpha to all takers.

### Copy & paste
Last week I decided copy-paste functionality is sort of vital after all, so I added it for the alpha (instead of leaving it for later).
This means I needed to add selection support, respecting the wrapping logic I already have.
This functionality is mostly needed in the alpha to copy parts of solutions from one puzzle to the next, but obviously it's also useful in lots of situations.

<video src="/assets/2017-09-15/select-copy-paste.mp4" controls loop autoplay></video>

For the very first alpha it'll be limited to keyboard selection only, boooooo. But cheer up, I'll add mouse stuff soon after, I'm not a total vimvangelist.

I'll also be adding much more sophisticated code management systems to the game, I'm envisioning versioned user-libraries that you can add to your solutions. I imagine alpha testers will be full of ideas on this.

### Next steps
I've pretty much wiped everything off my *alpha-1-todo-list*, everything except **tutorial**. So after a couple of weeks of sheepishly mentioning it I'll be actually tackling these vital intros to the world of robo-instructing next week.

**If you'd like to help me test the very first version please get into contact using one of the methods on the [front page](/)**.
*It's the little grey circles near the top. Did you notice they're not even images. They're scalable glyphs on a css-ed background. What a bloody hero huh?!*
