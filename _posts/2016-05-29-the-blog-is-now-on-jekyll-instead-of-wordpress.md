---
title: The blog is now on Jekyll instead of Wordpress!
date: 2016-05-29T19:51:00+00:00
author: Gjermund Bjaanes
layout: post
permalink: /the-blog-is-now-on-jekyll-instead-of-wordpress/
categories:
  - Uncategorized
---
The blog now has a brand new technology stack associated with it.
 
Previously I have used the oh-so-popular CMS, Wordpress.

Now I am using the much simpler static website generator, Jekyll.
    
<!--more-->
I even moved the hosting over to Github!

The new site is not quite polished yet. Some of the content might look a bit wierd and some design stuff is not like I want it, but it's a good start!

I'll also explain why I did this change, first I want to explain the differences between these.

# CMS vs static website generator

Wordpress is a full-blown Content Management System (CMS) that can do basically anything you can think of.

It runs PHP on the back-end and has a database where all my data is stored. 

It requires quite a bit of maintenance in terms of upgrades, fending off Wordpress-related attacks (had quite a few of them) and just different kind of admin tasks.

Granted, it doesn't take a lot of time, but it's time I'd rather spend doing something else.

[![Jekyll Logo]({{ site.baseurl}}/img/posts/jekyll-logo.png)]({{ site.baseurl }}/img/posts/jekyll-logo.png) 

Jekyll on the other hand is a static website generator. That means that it generates a website in HTML, and everything is served directly to the user.

In other words, after the site has been "built", every post has their own HTML page. The server only needs to serve those files to the users.

No database needed. No backend logic needed. 

And it's very fast. After all, it's only HTML files that needs to be sent back for every request.

No need to run tons of PHP script. No need to hit any databases.

&nbsp;

That said, Wordpress is not useless. Quite the opposite actually. It's very easy to get started with.

It can give you so many things with hardly any up-front work. Just install a plugin and you have new functionality on your site.


# Why I made the switch

The primary reason I switched was actually because of attacks. My site was under constant Wordpress-related attacks.

The amount of traffic alone from attacks have shut my site down several times a week.

The more secondary reasons are

* I didn't need Wordpress. It's just plain overkill for a simple blog like mine.
* Every post is Markdown. That means that I could more easily move my content to another technology stack later if I wanted to.
* All the content is on Github. The entire site is actually on Github. And that is awesome because:
    * Everything is source controlled
    * I can publish with "git push"
    * I can accept pull requests (to fix spelling mistakes for instance, or even new posts if someone wanted to write one)
    * Less backup to worry about (I trust Github <3)

These things combined make the move a very happy one from my part, even though it has been some work.

I will go into more detail about this in another post, but I had to do things like:

* Set up the project
* Convert my content to Markdown
* Set up a new theme
* Move Disqus over to the new site

# Forward

Like I said, the site still needs a bit of work to be "perfect", but I just wanted to release it!

The design is still a little rough around the edges (I used theme as a basis) and the content have some bad links and such.

But I like this approach so much better than Wordpress, and I am really happy with it!

How about you? Do you have a blog site on Wordpess and considered moving to something else?


