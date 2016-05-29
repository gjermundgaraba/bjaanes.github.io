---
id: 594
title: 'Learning Web Dev Series &#8211; Part 7: Parse shutting down'
date: 2016-02-21T12:42:33+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=594
permalink: /learning-web-dev-series-part-7-parse-shutting-down/
suevafree_template:
  - right-sidebar
dsq_thread_id:
  - 4598135538
categories:
  - Uncategorized
tags:
  - Express
  - Javascript
  - Node.js
  - Web
  - Web Dev Series
---
For my <a href="http://gjermundbjaanes.com/learning-web-dev-series-part-5-extreme-results/" target="_blank">Extreme Results project</a>, I have used Parse as my Backend-as-a-Service (BaaS). 

When they recently <a href="http://blog.parse.com/announcements/moving-on/" target="_blank">announced that they were shutting down</a> I was quite disappointed.

<!--more-->
Annoying to have a big part of your application pulled from underneath you.

&nbsp;

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/02/ripparse.png" rel="attachment wp-att-603"><img class="alignnone  wp-image-603" src="http://gjermundbjaanes.com/wp-content/uploads/2016/02/ripparse.png" alt="Rip Parse" width="319" height="391" /></a>

&nbsp;

# The choices

When this happened I basically had three options:

  1. Host my own Parse server
  2. Switch to another BaaS
  3. Create my own server from scratch

&nbsp;

## Option #1 Host my own Parse server

Option #1 is available because Parse has open sourced their server to allow people to migrate their existing apps. They have even create a <a href="https://github.com/ParsePlatform/parse-server/wiki/Migrating-an-Existing-Parse-App" target="_blank">migration guide</a> (which I guess is nice of them).

Luckily, Extreme Results is not in production, so I didn’t _have_ to choose this.

I didn’t really want my brand new application to have a dead backend. A backend with potentially no new updates. Option #1 just rubbed me the wrong way. It didn’t _feel_ right.

&nbsp;

## Option #2 Switch to another BaaS

Option #2 would require me to rewrite all the cloud code and migrate the data model to someone else’s backend framework. Might not be too much work, but certainly more than option #1.

There would however still be to possibility that a new BaaS could shut down and leave me where I’m right now. Not ideal.

&nbsp;

## Option #3 Create my own server from scratch

For learning purposes, option #3 is certainly the best choice. It would require a lot more work though.

It would allow me more control of the backend, potentially allowing me to create a even better backend.

&nbsp;

# The choice

With the following pros and cons in mind:

&nbsp;

## Hosting my own Parse server

  * Pros 
      * The fastest way to get up and running again
      * The “easy” choice
  * Cons 
      * Dead platform
      * Would need to deploy it myself

&nbsp;

## Switch to another BaaS

  * Pros 
      * Fast to get up and running compared to writing everything myself
      * No deployment and scaling to worry about (probably)
  * Cons 
      * Might shut down at any time
      * Potentially more expensive than Parse and creating and deploying my own server

&nbsp;

## Create my own server from scratch

  * Pros 
      * Amazing learning opportunity
      * Any functionality I can think of
      * Very flexible
      * Would never be shut down by someone else
  * Cons 
      * A lot of work
      * Would need to deploy it myself
      * Would need to scale it myself

&nbsp;

I chose **option #3** &#8211; creating my own server from scratch.

The pro I weighted most was the possibility to learn new stuff. It was just too good an opportunity to pass on.

&nbsp;

# Extreme Results Server

The were a lot of choices to be made once I decided to write everything myself. Not all choices are made yet, but at least enough to get started.

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/02/1436439824nodejs-logo.png" rel="attachment wp-att-595"><img class="alignnone wp-image-595 " src="http://gjermundbjaanes.com/wp-content/uploads/2016/02/1436439824nodejs-logo.png" alt="Node.js Logo" width="292" height="146" /></a>

The server is being written in Node.js with Express.

I wanted to do it like this, because then I could learn even more JavaScript (which is fun!). I could also leverage my experience with Jasmine for unit testing.

&nbsp;

I am currently writing unit tests and integration tests for the first Outcome API’s, and it is coming along nicely. It is actually pretty quick to write Express apps once you learn the basics.

&nbsp;

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/02/pluralsight_Inline_01.jpg" rel="attachment wp-att-596"><img class="alignnone wp-image-596" src="http://gjermundbjaanes.com/wp-content/uploads/2016/02/pluralsight_Inline_01.jpg" alt="Pluralsight Logo" width="455" height="142" /></a>

To actually learn some of this new technology I used a Pluralsight course called <a href="https://www.pluralsight.com/courses/node-js-express-rest-web-services" target="_blank">“RESTful Web Services with Node.js and Express”</a> by Jonathan Mills. It teaches the basics of Express and Node with along with some unit and integration testing.

&nbsp;

I am not sure how I will deploy the server for production and testing environments, but I hear Heroku might be a good fit.

The code is as always hosted on Github:
  
<a href="https://github.com/bjaanes/ExtremeResults-Server" target="_blank">https://github.com/bjaanes/ExtremeResults-Server</a>

&nbsp;

# The Journey – Visualized

I have a visual aid to help show where I am currently at on my journey. I have created a “prezi” presentation to visualize my path more clearly. It will be updated through the course of this series – so it might be longer than the current post you are reading.

<!-- Generated using Prezi Embedder. Get yours here: http://wordpress.org/plugins/prezi-embedder/ -->

&nbsp;

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_62">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Flearning-web-dev-series-part-7-parse-shutting-down%2F&linkname=Learning%20Web%20Dev%20Series%20%E2%80%93%20Part%207%3A%20Parse%20shutting%20down" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Flearning-web-dev-series-part-7-parse-shutting-down%2F&linkname=Learning%20Web%20Dev%20Series%20%E2%80%93%20Part%207%3A%20Parse%20shutting%20down" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Flearning-web-dev-series-part-7-parse-shutting-down%2F&linkname=Learning%20Web%20Dev%20Series%20%E2%80%93%20Part%207%3A%20Parse%20shutting%20down" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>