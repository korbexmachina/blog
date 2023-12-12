---
title: Too Much Configuration?
slug: too-much-config
date: "2023-09-04"
description: Is there such a thing as too much configuration?
---

Is there such a thing as too much configuration?

I have spent a lot of time editing config files, especially for certain programs (Looking at you Neovim & Kitty).
In the following blog post, I want to try and reason whether it was worth the effort, or if I would be better served sticking with a more impersonal, vanilla configuration.

## Background

The question of whether there is such a thing as too much configuration came to mind after I rewrote my [Neovim config](https://github.com/korbexmachina/nvim) from scratch yesterday (because it had become bloated and difficult to maintain), and realized how many plugins and custom keybindings I had set up, but never found myself using.
I spent hours upon hours fine-tuning that first config to perfection, or so I thought. What really happened, was that I ended up with a mess of spaghetti-like Lua that I couldn't debug effectively. I was trying to make my text editor do everything, when what I needed was simply a program that could effectively edit text.

My new config is paired down to what I feel are the core elements of my workflow, nothing more, nothing less. The best part? I only spend a couple of hours setting it up, getting it to a point where I won't have to mess with it for a long time.

## Conclusion

So, do I think that there is such a thing as too much configuration?

Yes, absolutely.

Do I think a more vanilla configuration would serve me better?

No, I think that spending a little bit of time setting up a program in a way that works for me is inherently valuable. It gives my a chance to dig in to the software and find out what is possible; and arguably most importantly, keybindings and other option that make sense to someone else are not necessarily intuitive for me.

Do I think that my initial Neovim config was a total waste of time?

No, I learned a lot in the time that I spent on that first config. It meant that I was able to work out what I actually needed this time around.
I also learned what not to do, so that I could write a more maintainable config this time.

I think the biggest takeaway is that I should keep the Unix philosophy in mind more often:

> "Make each program do one thing well."
>
> Doug McIlroy (Bell System Technical Journal, 1978)

## Thoughts

What do you think? Yes, you, the one reading this.

Is there such a thing as too much configuration?

Have you also fallen into a bottomless pit of configuration?

Let me know in the comments!

-Korben
