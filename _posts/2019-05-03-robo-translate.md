---
preface: robo-2
title: robo_translate()
excerpt_separator: <!--more-->
---

This week I've been working on translation systems for Robo Instructus. Today's **beta-1.10** update brings very early, work in progress interface translations for _Русский_, _Polski_ & _Deutsch_.

![](https://user-images.githubusercontent.com/2331607/57151015-c3a80a00-6dc7-11e9-8f81-a5503659e6e0.jpg "Baby steps to localization")
<!--more-->

## Machine translations, help if you can
The translations have been generated with google translate, so they'll be quite poor quality. If you are multilingual maybe you can help improve them, head over to [big-ab-games/robo-instructus-translation](https://github.com/big-ab-games/robo-instructus-translation) and take a look at the ~70 words and phrases currently translated.

As a solo dev with limited resources I may not be able to fund many professional translations, so community help could provide a route to a translated Robo Instructus that otherwise wouldn't exist.

![](https://user-images.githubusercontent.com/2331607/57151036-d3bfe980-6dc7-11e9-9615-191429502853.jpg "Cheeky warning so you're not too disappointed with the current translation")

Regardless of the quality, the current translations are a decent test of the new translation _systems_.

## Dealing with translated text
Along with the obvious difficulty of getting good quality translated text, localization presents a bunch of other issues, particularly for a lowish level game like Robo Instructus.

The game needs a system to spit out different text based on current language. Once you have that you may find the translated text takes up much more space and maybe doesn't work. Some languages use alphabets that the font might not even support, or maybe some fonts do and others don't. Tweaks may need to be applied to different fonts and language text.

![](https://user-images.githubusercontent.com/2331607/57151057-e5a18c80-6dc7-11e9-92c1-e8d1de5264b6.jpg "This probably needs to be nudged down a bit...")

This is partly why I've started with only 3 new languages and in a very limited way. Lots of the game remains English only, but the translation system can be extended and improved to cover everything.

## Quality & professional translations
I'm keen to do as I can to make high quality localized versions of Robo Instructus. When it comes to technical barriers I will work hard to remove them. However, ultimately I won't be able to afford professional translations for the full game in every language. I think community translated menus & such can work, as the workload is quite small. These UI bits are also important to get right, machine translations won't do.

The game story though is much longer and more difficult to handle. There may be an option of having sort of in-game machine translations for the story, as if you've discovered a colony that speaks a foreign language and you have to use your translation tools. I'll look into this though I do wonder if it'll actually appeal to many.

I do think having a good interface translation has value, even if the rest of the game remains in English. With a little help I don't see why the game can't have decent UI localization for every language I can render.
