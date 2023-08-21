---
title: Creating a Blog with Hugo
slug: hugo-blog
date: "2023-08-21"
description: My experience creating my blog site with Hugo.
---
## Why Hugo

Honestly I kind of chose it on a whim. I was researching various static site generators, when I came across Hugo. Not only did it seem to fit my use case perfectly, it was written in my favourite language! After using Hugo for a while, I feel like I made the right choice. I have fought with it at times, but usually the answer was easy to find in the official documentation.

This blog uses a theme called [Poison](https://github.com/lukeorth/poison), I found the configuration for this to be mostly straightforward. I am using [Utterences](https://utteranc.es/) for the comments, I had to make a few minor changes to the theme for the comments to work properly.

Something that I really appreciate about Hugo is the out-of-the-box RSS feed support. I want to share my content with others, and I think it's important that they are able to view it comfortably, so having an RSS feed for my blog was a must from the start.

## Challenges

- For a while I was struggling to get the main image to resolve properly on all pages, but this seemed to fix itself eventually
- It took me longer than I would like to admit to figure out that I had to change the base URL in hugo.toml in order to make all of the pages resolve properly.
- Setting up Utterences took me a little while, I had to dig through some files in the theme, since it did not support Utterences out of the box.
    - It was worth it because I want to provide this site for free, and I also do not want to embed trackers or ads in order to offset the cost of a different commenting solution. I also like the idea of having all of the comments stored in the repository.
