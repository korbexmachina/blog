---
title: My Developer Toolkit
slug: toolkit-2023
date: "2023-08-22"
description: A brief rundown of the tools I use as a developer.
---

I want to use this post to give my future self, and anyone else who might be interested, a look into what my developer toolkit looks like after my first year of college as a Computer Science major.

## What are the tools?

First of all, the tools I use every day. These are what I consider to be the core elements of my workflow.

- Git (obviously)
- Neovim (The best thing since Vim)
- Tmux (A brand new addition)
- Zsh (My favourite shell)
- Homebrew (A wonderful package manager)
- Kitty (A modern terminal)

Next, let's take a look at the other tools that I use frequently, but that my workflow is not totally dependant on.

- Bat (Better than `cat`)
- Starship (Cross platform shell prompt)
- fzf (Fuzzy finding!)

Finally, what languages amy I using right now?

- Go (My new favourite language)
- C (Old Reliable)
- Python (Automating basic tasks)

Obviously this isn't everything. However, this is intended to be a snapshot of the important things, not every single package I have installed with Homebrew.

### Let's talk about them!

First up is Git. I really don't think I need to explain why Git is crucial to my workflow, suffice it to say, I don't think I could build anything remotely complex without it.

Next on the list is Neovim. I love Vim keybinds, and I'm always improving my speed with them. The addition of Lua support make configuration so much more straightforward, and it is the main reason I chose Neovim over Vim.

Next up is Tmux. Tmux is actually new to my workflow, it replaced Zellij as my multiplexer, and after configuring it with some Vim-stlye keybinds, I find it quite intuitive to use, in a way that Zellij never was for me.

I have been using Zsh for a long time now, and I really see no reason to go back to Bash.

Homebrew is a really solid package manager, it was also the first package manager I really used, aside from apt in the occasional Ubuntu VM. Now that I have lived a little more, and sampled lots of different package managers, I feel good saying it is one of my favourites.

Kitty is the fastest terminal emulator I have ever used. I don't know how I ever lived without it.

Bat is a really pretty way to dump the contents of a file into the terminal. It is one of my favourite examples of "Rewrite it in Rust", since it builds on the functionality of cat, rather than just mirroring it.

Starship is a great prompt, and is extremely customizable. My current config is very minimal though.

I dont find myself using fzf a lot, but when I do, I am extremely grateful it's there.

Finally, let's take a look at the languages I'm using right now:

- Go is an absolute pleasure to work with, and I think it strikes a good blance between development speed and runtime speed. I also appreciate how easy it is to target multiple operating systems, while still compiling to a native executable.
- C really is a workhorse. I honestly enjoy working with it too, granted not quite as much as I enjoy Go. I really need to work on my Makefile skills though.
- Python is a great programming language for writing small programs as quickly as possible. However, in my experience, packaging it for distribution is an absolute nightmare compared to compiled languages. This is the main reason I don't use it as often anymore.

Of course, there are other languages I work with here and there, but these are the three that I use most frequently; a year ago Java would have definitely made this list.

## Farewell to some old friends

Since this is the first one of these posts (buckle up, I intend to write at least one per year) I want to take a look at some things that left my toolkit this year.

- GitKraken (I live in the terminal now)
- VScode (Once I got used to Vim, there was no going back)
- Zellij (I just prefer Tmux)

I want to say that I don't think that any of the tools listed above are bad, they just aren't for me.

GitKraken in particular is a brilliant application, providing my favourite GUI for git. However, as I began spending more time in the terminal I found myself reaching for GUI's less and less.

I used VScode for a solid year, I started using it because it was much lighter and faster (see where this is going?) than the JetBrains IDE's I was using at the time. Eventually I felt dissatisfied with how slow it was as well as the weird combination of GUI and text file configuration required to get it just right. I had heard about Neovim in various places online, including seeing it listed as the "Most Loved Editor" among Stack Overflow users. Eventually I decided to give it a try and cloned [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim) as a starting point for my configuration. I have since made a lot of changes to my config, and I intend to rewrite it from scratch using what I have learned, but kickstart gave me evrything I needed to get started, and I highly recommend it if you are interested in trying Neovim.

Zellij was actually a relatively new addition to my toolkit, I believe I started using it in March. I  really enjoyed my time using it, and I highly recommend it to anyone who wants something a little more beginner friendly than Tmux. I switched to Tmux for a couple of reasons. First, Tmux integrates better with Neovim. Second, Zellij wastes a little too much screen space for my liking; I felt like I was working in a series of little boxes, it was a bit claustrophobic to be honest. Overall though, I think zellij is a wonderful tool and I definitely still recommend it.

That's all for now!

-Korben
