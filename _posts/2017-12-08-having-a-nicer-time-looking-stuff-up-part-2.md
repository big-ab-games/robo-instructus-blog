---
preface: robo
---

Today Robo Instructus _alpha-1.6_ has landed. It brings the first complete implementation of the reference system I've been talking about in previous weeks. This is an important quality of life improvement for the game, lets take a look!

![](/assets/2017-12-08/api-ref-screen.png "Shiny new reference")

New in _alpha-1.6_ players can open a reference in the right hand side of all the tutorials. This allows you to look up stuff and code at the same time. Toggle the reference with the **F1** key.

The implementation took quite a long time with holiday bullet holes notching my armour of productivity, also for a seemingly simple addition it included quite a lot of subtlety. I had to formalise my simplistic markup notation to allow it to be mixed up, indexed and rendered all as one scrollable mass (instead of a single page).

<video src="/assets/2017-12-08/api-ref-1.mp4" loop autoplay></video>

The new reference also integrates with _alpha-1.5_'s function summary. A click on a function name in the summary will open and take you to the relevant section of the reference.

<video src="/assets/2017-12-08/api-summary-to-ref.mp4" loop autoplay></video>

Alpha testers please give this a spin and let me know what you think!

### Coming up
With the reference implemented I can regroup my thoughts and move to the next significant improvement to the game. Expect new stuff next week.
