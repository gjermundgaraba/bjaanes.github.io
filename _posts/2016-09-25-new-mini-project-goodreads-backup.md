---
title: 'New Mini Project - Goodreads Backup'
date: 2016-09-25T13:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /new-mini-project-goodreads-backup/
categories:
  - Uncategorized
tags:
  -
---
I have just started a small project which I wanted to share with you. I also hope to get some feedback or ideas.

The idea for this project started when I noticed that the counter on my Goodreads account was off.
It was missing a book. I went through the list, and all my books were there, but the counter was wrong.

<!--more-->

![Goodreads Logo]({{ site.baseurl}}/img/posts/goodreads-logo.jpg)

This little bug, which seemed like it could affect my data, coupled with the slightly buggy Goodreads app,
made me want to backup my data.

After all, I keep my lists of books I want to read there, and the books I have read. I don't want to lose that.

In short, I don't really trust Goodreads to keep my data safe, so why not just back them up myself?

&nbsp;

# Plans for the project

I plan on using Goodreads API's to fetch all the books that are in my lists, and persist them (in some yet-to-be-determined way).

I am not sure if the application should be some sort of background daemon that syncs periodically,
or if it should be a one-off application you use to download all your lists into a file or something.

I am currently leaning towards a syncing daemon that just sits in the background on some server and keeps my data safe,
but I haven't concluded on anything just yet.

Perhaps it should somehow sync it to Dropbox? Yeah, not sure yet.

I have also thought about using the data for other purposes,
but I haven't managed to create a clear picture for any use cases yet.
That is the sort of thing that comes better into view after some exploration.
That's why I'll just create the backup functionality first.

&nbsp;

# The code

The code is as always available on GitHub:
[Goodreads Backup on GitHub](https://github.com/bjaanes/goodreads-backup){:target="_blank"}

The project is being written in Python, because I am trying to learn myself some Python. It's an interesting language that reads nicely. Plus, learning new things is always fun.

There is not much code yet to speak of. I am adding bits and pieces when I have the time.

Hopefully I will get it functional soon. At least the basic functionality; saving my data.

If you have any ideas or want to contribute, feel free to reach out! It could be a lot of fun!
