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

So these guys are having all my data, eh?

<!--more-->

![Goodreads Logo]({{ site.baseurl}}/img/posts/goodreads-logo.jpg)

This little bug, which seemed like it could affect my data, coupled with the already buggy Goodreads app,
made me want to backup my data.

After all, I keep my lists of books I want to read there, and the books I have read. I don't want to lose that.

In short, I don't really trust Goodreads to keep my data safe, so why not just back them up myself?

&nbsp;

# What the script does

The script is not too complex, all it does is the following steps:

1. Fetch a given users books and shelves using the Goodreads API
2. Aggregate all books into a format I can use (not XML)
3. Save each shelve to each it's own CSV file

So basically, all I needed to do was to use a REST API from Goodreads, read some XML and save it to a more suitable format.

&nbsp;

# Plans for the Project

I have created a web frontend for the project, which I wrote about in [Goodreads Backup - With a web app]({{ site.baseurl}}/goodreads-backup-with-a-web-app/){:target="_blank"}.

This frontend makes the script a bit more user friendly, but I want to create an automated process for this as well. 
I might just use one of my existing VPS to periodically download all my shelves.

Or I might create something more people can use - we'll see.

&nbsp;

# Open Source - of course

The code is as always available on GitHub:
[Goodreads Backup on GitHub](https://github.com/bjaanes/goodreads-backup){:target="_blank"}

The project is being written in Python, because I am trying to learn myself some Python. It's an interesting language that reads nicely. Plus, learning new things is always fun.

If you have any ideas or want to contribute, feel free to reach out! It could be a lot of fun!
