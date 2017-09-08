---
preface: robo
---

So you finished the level, *welly welly done done*. **But was you solution really any good?**
<br/>This week brings 'Level Complete' dialogs and solution performance statistics to Robo Instructus. Now you'll see just how bad your code is compared to Elizabeth's.

![](/assets/2017-09-08/level-complete-screen.png "Stats!")

The current stats represent the time it took to complete this levels, that is the total of all the variants until the end. Moving about, scanning and all the rest have a cost - they take time. Clearly we'd like to take as little time as possible.

By gathering & exposing these I can build in auto comparisons with your best scores, your mates' best and the world's best!
I could also build in some fixed targets as encouragements to optimise. For the alpha builds, however, it'll just be the numbers. Staring at you. Asking to be smaller.

The stats themselves are deterministic & based on your calls to the ***robo_**** APIs, so changing the speed of execution, robot movement, or pausing the code will *not* affect the outcome.

<video src="/assets/2017-09-08/level-complete.mp4" controls loop autoplay></video>

### Clipboard
I had initially left copy-paste functionality off my alpha features, but I've decided this will be too annoying in it's absence. I mostly boshed out the code yesterday anyway, so not a huge deal after all. This should be ready next week.

### Open source
As a huge beneficiary of amazing open source code (as we all are really) I'm keen to contribute where I can. While Robo Instructus itself is closed source, the general purpose parts I develop along the way I will actively open up & shove on github. Since I'm developing Robo Instructus in [rust](https://www.rust-lang.org), this mean rust crates.

I have a few projects you can find [on github](https://github.com/alexheretic). Highlighting one of the simpler ones; I've recently added a helper for reporting frame rates in a convenient way to my rust library [spin_sleep](https://github.com/alexheretic/spin-sleep).
This tiny crate could be useful for FPS reporting in anyone's rust games & experiments, I'm using it to calculate & update compute & frame rates in Robo Instructus.

```rust
// rust
extern crate spin_sleep;
use spin_sleep::LoopHelper;

let mut loop_helper = LoopHelper::builder()
   .report_interval_s(0.5) // report every half a second
   .build_with_target_rate(250.0); // limit to 250 FPS if possible

loop { // game loop
   let delta = loop_helper.loop_start(); // or .loop_start_s() for f64 seconds

   // compute_something(delta);

   if let Some(fps) = loop_helper.report_rate() {
       update_fps_display(fps);
   }

   loop_helper.loop_sleep(); // sleeps to acheive a 250 FPS rate
}
```

I've also made performance improvements and fixes to my glyph rendering crate [gfx_glyph](https://github.com/alexheretic/gfx-glyph) this week.

So the Robo Instructus first alpha continues to shape up. Are you ready to help me test it? As ever, if you like reading about the game or want to help me out, head over to [facebook](https://www.facebook.com/alexbutlergames) or [twitter](https://twitter.com/alexbutlergames) and like/follow/comment. Doing this will really help me build the buzz for this engineering puzzler.

##### Comment on [reddit](https://www.reddit.com/r/devblogs/comments/6yugy6/robo_instructus_adding_performance_statistics_how/) | [twitter](https://twitter.com/alexbutlergames/status/906133079705694211) | [facebook](https://www.facebook.com/alexbutlergames/posts/1584201418333906)
