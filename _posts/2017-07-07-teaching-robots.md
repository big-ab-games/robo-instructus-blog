Last week I was talking about some [advantages of letting players write code](/2017/06/30/coding-in-the-game.html), but what was I really getting at?

### Talking to the game
I'm convinced there's legs in the idea of coding inside a game as a primary input. That is instead of relying on direct control of the player character, as most games do, you can explain to the game what you'd like to happen. This is the end I've been pursuing for the last month.

I see a lot of potential in this. I think it can really explode the power of a player in a game world, and in lots of different ways. What if you could be a real engineer or magician, actually creating your own world affecting inventions instead of just using pre-created actions, rolling a virtual die or doing abstract mini-games? Perhaps you could end up doing stuff even the game creator hadn't imagined.

But before I disappear into the [Molyneux](http://kotaku.com/the-man-who-promised-too-much-1537352493) clouds, I need to see if the basics work. So I cut down the idea into the simplest implementation of a fun game.

### The Idea: Instructing Robots
Riffing on the gaming classic *get to the end of the level* puzzle, you have a little robot and you need to get him to the exit. However, yes you guessed it, you can't actually move him about directly. He's a robot mate, **you're going to need to code**.
<br/>Moreover, you'll need your program to get the robot to the exit of *multiple similar levels*.

So in the game you can write your code on the left hand side, and see the game world on the right. You submit your program and see what happens to the brave little robot. Hmm I wonder what happens if he gets to an edge and- OH GOD HE FELL OFF THE EDGE.

![](/assets/2017-07-07/sketch.png "Not actual game footage")

When you execute the program you'll see the code running, see the robot moving about according to the program. At the end of each set of levels you can see your program's performance. Was it fast? Was it graceful? Or more importantly was it better than Barry's attempt?

As you progress more dangers will block you. You'll get new abilities. You'll need to help out different robots with new APIs, that is new sets of abilities you'll need to exploit in your programs.

### Progress
Let me show you my current progress. **Please note this is a super early version & all art is placeholder!**
<video src="/assets/2017-07-07/progress-600k.webm" controls></video>

This video introduces:
* *Badder* a programming language I invented for the game *(more on that later)*.
* Visual program execution, we can see what bit of code is being evaluated. In addition to what is shown, players can also change the execution speed, or pause it altogether.
* Interlocking tile based level layouts rendered in isometric 2D. This perspective at least will stay, while the art can be replaced later.
* Temporary pixel art from my very own hand, in particular **Placeholder Panda** fulfilling robot duties. I didn't have time to properly animate him, so he's currently always watching you.

As you can see the current build hasn't actually got a game in it yet. I'll be working on the initial level(s) in the coming weeks. However, I hope you can start to see what I'm working towards. Lets see what next week brings!

##### Comment on [twitter](https://twitter.com/alexbutlergames/status/883307001719250944) | [facebook](https://www.facebook.com/alexbutlergames/posts/1497823606971688) | [reddit](https://www.reddit.com/r/devblogs/comments/6ltfzh/that_guy_that_quit_his_job_to_make_games_teaching)
