---
title: Creating a Blog with Hugo
slug: hugo-blog
date: "2023-08-21"
description: My experience creating my blog site with Hugo.
---
## Why Hugo

Honestly I kind of chose it on a whim. I was researching various static site generators, when I came across Hugo. Not only did it seem to fit my use case perfectly, it was written in my favourite language! After using Hugo for a while, I feel like I made the right choice. I have fought with it at times, but usually the answer was easy to find in the official documentation.

This blog uses a theme called [Poison](https://github.com/lukeorth/poison), I found the configuration for this to be mostly straightforward.

Something that I really appreciate about Hugo is the out-of-the-box RSS feed support. I want to share my content with others, and I think it's important that they are able to view it comfortably, so having an RSS feed for my blog was a must from the start.

## Challenges

- For a while I was struggling to get the main image to resolve properly on all pages, but this seemed to fix itself eventually
- It took me longer than I would like to admit to figure out that I had to change the base URL in hugo.toml in order to make all of the pages resolve properly.

## Next Steps
- I want to implement comments, probably using [utterances](https://utteranc.es/)
