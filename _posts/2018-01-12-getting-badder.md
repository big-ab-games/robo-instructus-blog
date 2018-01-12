---
preface: robo
---

The central feature upcoming robot commanding romp _Robo Instructus_ is the bespoke programming language _'badder'_ created for the game. It's a language I designed to have a very small tight core feature-set. This core is comparatively quick to learn and once done you're free to mess up the puzzles with terrible algorithms.

```rust
loop
    var scan = robo_scan()
    if scan is 1 or scan is 2
        robo_forward()
    else
        robo_left()
```

### Badder goals
Generally I believe creating your own language is pretty silly, there are many great ones already made by cleverer people, still I did it anyway. I wanted total control of the language so I could strip it down to the smallest core possible, so I could support all the runtime/highlighting/debugging requirements I had and to mix the idea I thought made a language easiest to learn and read.

<video src="/assets/2018-01-12/run.mp4" loop autoplay></video>

### A small core
The _'core'_ of a language is the bit you need to learn before you can think in it. Normally that means learning the syntax, core concepts and standard library. Once you've fluent in the core of a language you experience a really freeing feeling of being able to do whatever you need.

However, the road to core-fluency can be a little long for many languages, particularly the first time. So _badder_ tries to minimise this as much as possible, whilst still being a language you can actually use to express the algorithms required by the game.

I won't go into it all, you'll have to play the game instead, but for example, the badder standard library has only 3 functions. All 3 are for basic sequence functionality, ***size***, ***add*** and ***remove***. Really you just learn them along with the sequence functionality. The idea is that any functions you need you just write yourself, building up in this way you'll get a appreciation of the satisfaction, importance & difficulty of abstraction.

So if you want a ***contains*** function, write it yourself:

```kotlin
fun contains(items[], it)
    for item in items[]
        if item is it
            return 1
    return 0
```
And use it:
```kotlin
seq safe_tiles[]

if safe_tiles[].contains(robo_forward_location())
    robo_forward()
else
    robo_left()
```

### Language distinctive features
Badder is a mongrel child of many language ideas. We have python style whitespace scoping, javascript/kotlin/scala-like ***var*** declaration, conventional c-like syntax names ***if***, ***else***, ***for*** and function calling, ***'and'***, ***'or'*** words instead of symbols. In general _badder_ should be familiar to most code dabblers.

However, it does differ in some respects. Badder is integer only, all ***var*** ids are just numbers. ***seq*** declare sequences, these must have an id ending in ***[]*** _(ie **safe_tiles[]**)_. In this way sequences are syntactically distinct from variables in a way not normal in programming languages. But this does mean the code becomes a little more obvious to read. Actually this would be hard to do in most languages, as they have many types. So its a luxury of simplicity.

I also added two ways to call a function with arguments. Either normal
```kotlin
my_func(1, 2, 3)
```
Or dot style, where the first argument goes in front:
```kotlin
1.my_func(2, 3)
```
Why? Well some functions read better this way, _don't you think the **contains** function above is better like that?_

### Coding is fun?
That's the idea yes, that all this will be fun for players to work out. I remember writing about this [last year](/2017/06/30/coding-in-the-game.html). Ultimately I want players of Robo Instructus to leap the hurdle of learning _badder_ and enjoy using the it to solve the game's puzzles. All this design is to make that more possible for more people.

### Progress
Currently I'm working toward alpha-2, described in last weeks: [2018 goals](/2018/01/05/2018-plans.html). However, I also released _alpha-1.9_ with some new fixes and minor features to my alpha testing group earlier today. I'm still very interested in feedback from alpha-1.x so please do get into contact if you want to help me make this game better.

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/7pya2v/robo_instructus_getting_badder_a_look_at_the/) | [twitter](https://twitter.com/alexbutlergames/status/951873457511370753) | [facebook](https://www.facebook.com/alexbutlergames/posts/1742220369198676)
