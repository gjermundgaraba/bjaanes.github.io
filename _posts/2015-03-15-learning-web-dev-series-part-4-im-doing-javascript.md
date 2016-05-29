---
id: 201
title: 'Learning Web Dev Series &#8211; Part 4: I&#8217;m doing JavaScript!'
date: 2015-03-15T10:27:18+00:00
author: Gjermund Bjaanes
layout: post
guid: http://maximumdeveloper.com/?p=201
permalink: /learning-web-dev-series-part-4-im-doing-javascript/
video_url:
  - 
audio_url:
  - 
quote_content:
  - 
quote_attribution:
  - 
link_url:
  - 
link_title:
  - 
dsq_thread_id:
  - 3596662704
categories:
  - Uncategorized
tags:
  - Programming
  - Web
  - Web Dev Series
---
I mentioned <a title="Learning Web Dev Series – Part 3: All That Front End" href="http://maximumdeveloper.com/learning-web-dev-series-part-3-all-that-front-end/" target="_blank">last time</a> that I had changed direction into a bit into more fundamentals. 

<!--more-->
I have also gotten more learning in since then. I have done almost all the courses I am interested in on codeschool.com. 

I will probably move on to Pluralsight after that. They seem to have a lot of great content.

The courses I have taken on codeschool since last time is:

  * JavaScript Best Practices
  * Staying Sharp with Angular.js
  * Real-time Web with Node.js
  * Bulding Blocks of Express.js

Not as many courses done as previously, but I have instead taken on a more "hand-on” approach with my learning (aka. I have coded more on my own stuff).

I have tried to learn as much JavaScript as possible, and it has truly been a blast!

&nbsp;

# AngularJS

My primary focus have been front end development - but even more specifically I fell totally in love with AngularJS. Its such a great framework. I haven't much to compare it with at this time (even though I have looked at some of the other popular in the space), but at least I enjoy it.

I have done most of my Angular learning on code school. I have also utilized the <a href="https://docs.angularjs.org/tutorial" target="_blank">AngularJS official tutorial</a>, <a href="https://docs.angularjs.org/guide" target="_blank">developer guide</a> and <a href="https://docs.angularjs.org/api" target="_blank">API Reference</a>. They have in combination proved to be a great way to learn the ropes (it was for me anyway).

After a while, when getting down into Angular i found that without a proper back-end I would come to a halt pretty soon.

&nbsp;

# Node.js

I spent some time looking at possible solutions for a back-end. I tried the Java route, but I don't really love their approach. It just takes too much time for a simple solution. I looked at Parse (which I already know pretty well) and FireBase as a BaaS (Back-end as a Service) solution, but it felt wrong; I didn't need anything super fancy - I just wanted a REST API I could use in my Angular app. Enters Node.js and Express.js.

It's so frickin' easy to create a simple back-end with node and express. Even getting up some persistence with MongoDB was a breeze. I mean, why make it complex and difficult if you don't really need all that complexity? I can fit my entire back-end logic into a small file as is (I will probably split it up later, but it works just fine for now).

I learned the basics of node and express from codeschool, and googled my way to using mongojs (a MongoDB driver for node). Real easy! And fun!

&nbsp;

# Show and tell

I really wanted to have something concrete to actually show you guys with this post, and I have! I have made a little learning project that I put up on my <a title="Angular Cards on Github" href="https://github.com/bjaanes/AngularCards" target="_blank">Github account</a>. It’s called AngularCards. It's nothing fancy and probably nothing anyone would use for anything, but it made for a great learning experience.

It uses AngularJS with some Bootstrap for all the front-end parts, and node.js, express.js and MongoDB for back-end. It’s actually the MEAN (MongoDB, Express, AngularJS and Node) stack.

The app istelf doesn't do anything too fancy. The app revolves around cards with text. The user can see all the cards laid out. Cards can be added, and deleted.

&nbsp;

[<img class="alignnone wp-image-202" src="http://maximumdeveloper.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.02.png" alt="AngularCards" width="748" height="435" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.02.png 1200w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.02-300x174.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.02-1024x595.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.02-945x549.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.02-600x349.png 600w" sizes="(max-width: 748px) 100vw, 748px" />](http://maximumdeveloper.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.02.png) [<img class="alignnone wp-image-203" src="http://maximumdeveloper.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.40.png" alt="AngularCards Add Card" width="750" height="435" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.40.png 1200w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.40-300x174.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.40-1024x595.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.40-945x549.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.40-600x349.png 600w" sizes="(max-width: 750px) 100vw, 750px" />](http://maximumdeveloper.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-15-at-10.16.40.png)

&nbsp;

# Next up

I am getting more exited about this learning journey for each day! I just wish I had even more time to commit to it. It's done entirely on my own time after work and it sometimes feel like I don't get as much done with it as I want (obviously).

That said, I am going to continue doing this, and I won't stop! I have a pretty huge project that I am working on, but I I'm not sure when I'll get the opportunity to show it. I want it to take some shape before I share it with the &#8216;world'. Rest assured, it will be entirely open, and also solving an actual problem of mine.

In terms of learning I have a couple more codeschool courses I want to take. I also want to learn more about web design. But my focus will certainly be coding (on the MEAN stack).

&nbsp;

# The Journey – Visualized

I have a visual aid to help show where I am currently at in my journey. I have created a “prezi” presentation to visualize my path more clearly. It will be updated through the course of this series – so it might be longer than the current post you are reading.

<!-- Generated using Prezi Embedder. Get yours here: http://wordpress.org/plugins/prezi-embedder/ -->

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_19">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Flearning-web-dev-series-part-4-im-doing-javascript%2F&linkname=Learning%20Web%20Dev%20Series%20%E2%80%93%20Part%204%3A%20I%E2%80%99m%20doing%20JavaScript%21" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Flearning-web-dev-series-part-4-im-doing-javascript%2F&linkname=Learning%20Web%20Dev%20Series%20%E2%80%93%20Part%204%3A%20I%E2%80%99m%20doing%20JavaScript%21" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Flearning-web-dev-series-part-4-im-doing-javascript%2F&linkname=Learning%20Web%20Dev%20Series%20%E2%80%93%20Part%204%3A%20I%E2%80%99m%20doing%20JavaScript%21" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>