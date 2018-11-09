---
preface: robo
---
This week it's time to compare your Robo Instructus solutions with all the other engineers. For the first time the game will connect with the outside world and start to answer the question: _Was that "Solution size: 51" stat I got at the end of the level good or bad?_

![](/assets/2018-02-24/graphs.png "Global stat graphs v1")

Previously you could write a proper affront to programming and as long as it solved the level you could think to yourself: "That was probably fine, it doesn't have to be perfect anyway. I'm having a good time".

**NOT ON MY WATCH.**

The idea is the game now uploads your best scores into the cloud, fetches a summary of all other players and shows where your solution stats fit with everyone else's. This is cool because it gives you an incentive to optimise your solutions. Optimising is fun!

Global stats are in the latest ***alpha-1.11*** release. All alpha testers should give this a go, plus re-run old solutions to upload them!

### Connecting with the cloud
I've been planning this feature since the beginning but it requires something nothing else in the game has so far: Connection with the outside world. Plus something in the outside world to actually connect to.

So we need something online that can store players scores & provide summaries of the global distribution so the game can draw nice graphs. Far from the world of sending triangles to graphics cards, I need a database in an internet.

Luckily, in my time as a enterprise dev I developed many opinions on scalable database design _and bear the scars of the endless arguments with architects about them_. Finally all that enterprising is useful! The money was nice too!

Oh god the money.

Anyway! How did I design my database? Bring on the ASCII diagram!

```
 AWS DynamoDB                             AWS DynamoDB
+--------------------+   Async update   +-----------------------+
| Best-score storage |  ------------->  | Global stat summaries |
+--------------------+                  +-----------------------+
          ^ AWS Lambda                             | AWS Lambda
          |                                        |
----------------------------Internet-----------------------------
          | upload best                            | Fetch latest global
          | scores                                 | score summary
          |                                        v
+---------------------------------------------------------------+
|                           The Game                            |
+---------------------------------------------------------------+
```

### Eventually consistent key-value goodness
Do you know what's fast in databases: Key-value lookup. Do you know what's scalable in databases: Key-value lookup. So if you can solve your read and write problems just doing a small amount of (hopefully one) key-value lookups you're probably going to be all right. This is what I've done for player scores in Robo Instructus.

When a player gets a new best score they send it to the best-score storage. Boom one key-value insertion.

When a player wants to look at a graph of everyone else's scores they request the summary from another service. _No put your SQL query away,_ boom it's another single key-value lookup. That's possible because the summaries get updated asynchronously by a backend service. This _eventual_ consistency is the secret sauce that makes all client interactions simple scalable and fast. That's the idea anyway.

I used AWS Lambda & DynamoDB which fit pretty nicely with this approach. Let's see how it goes as time goes on.

### Also the game
Yes I've been developing the game too. Last week I finished an arc of new, post-alpha, levels making use of the new tools I talked about in [Asking For A Little More](/2018/02/09/asking-for-a-little-more.html). Particularly there's one that will ask quite a bit more:

![](/assets/2018-02-24/new-level.png "This level is a bit hard")

This level is a fun one. You're really going to have your game on.

Next I'll spend some time polishing the new stat functionality and continue designing new levels & tools.

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/7zvng5/robo_instructus_stats_in_the_cloud/) | [twitter](https://twitter.com/bigabgames/status/967334949127847936) | [facebook](https://www.facebook.com/bigabgames/posts/1790377374382975)
