---
preface: robo
---

This week I've been working on expanding new meaningful metrics for successful solutions. Coming up with a solution that works is one thing, ***but was it such a great solution?***

![](/assets/2017-12-15/metrics.png "New ways to be bad at the game: metrics")

To find out how good a solution is the game already tracks how fast it is. Fresh in _alpha-1.7_ two new metrics have appeared. We have **Solution size** and **Run size**.

### New metrics

**Solution size** is roughly the size of your code. It isn't lines of code though, instead it's measured in nodes, kinda one per node on the abstract syntax tree. I.e. one per expression/statement. Trivial nodes are ignored, e.g. number literals and assignment _(so naming your numbers won't affect the score)_. It's really meant to be proportional to the grace of the code. A lower score is better!

**Run size** represents the how much code had to be executed before the level was completed. Lots of repeated computation will bump this way above the _solution size_. This number is the computation cost of the solution. Again a lower score is better!

It's always a little fraught trying to artificially value code, although here I have an advantage in that my analysis isn't static, it's based on the run that solved the level. In any case I'll probably be tweaking the stats to make sure they're fair and meaningful, I'd appreciate feedback! I may also blog about it more in a little more detail, we'll see.

Really the fun will start when players can properly compare scores to each other!

### Improved robo effects

I also want to improve the feedback & clarity of the _robo_xyz_ functions. I'm thinking effects that highlight the relevant tiles would help people learn how the game works, or fixing & improving their algorithms. I bundled a new effect for _robo_scan()_ in the latest alpha, but I still need to work on it and the others to make sure they don't look too naff.

<video src="/assets/2017-12-15/scan-lines.mp4" loop autoplay></video>

I'll keep working on effects for the other functions too, I'm convinced they help in visualizing what's happening. If I do a decent job with them they'll help make the game look a little more interesting too.

I'll have more to show off next week.

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/7k0zwc/robo_instructus_introducing_new_game_solution/) | [twitter](https://twitter.com/alexbutlergames/status/941716060805398528) | [facebook](https://www.facebook.com/alexbutlergames/posts/1711479208939459)
