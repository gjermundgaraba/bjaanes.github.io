---
id: 190
title: 'My favourite debugging technique &#8211; Code Evaluation'
date: 2015-03-08T17:18:41+00:00
author: Gjermund Bjaanes
layout: post
permalink: /my-favourite-debugging-technique-code-evaluation/
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
  - 3578434204
categories:
  - Uncategorized
tags:
  - Programming
---
My favourite debugging technique is using code evaluation at break points. 

What that means is that I put down a breakpoint somewhere in the code, and when the debugger hits that breakpoint I can pull up a code evaluator to evaluate basically any expression I want. 

<!--more-->
Using this code evaluator I can then write short code snippets / expressions to debug my code. 

I can query different objects and test values and what I can access from that particular point in the code. 

Most stuff you can do in code, you can do in code evaluation.

&nbsp;

You might have done this manually many times before. Perhaps writing a print statements that tests some variable? Perhaps putting querying lots of services to debug something? Doing that is OK, but it is also extremely slow. In huge systems, it might take quite a long time to build, set up and perform the deployment.

&nbsp;

I do not know how to do this in any other IDE than IntelliJ IDEA (however, I am sure it exists for Eclipse, NetBeans, Xcode and most other IDE’s worth their salt).

&nbsp;

[<img class="alignnone wp-image-191" src="http://maximumdeveloper.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-08-at-17.14.11.png" alt="Screen Shot 2015-03-08 at 17.14.11" width="880" height="562" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-08-at-17.14.11.png 1323w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-08-at-17.14.11-300x192.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-08-at-17.14.11-1024x654.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-08-at-17.14.11-945x604.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-08-at-17.14.11-600x383.png 600w" sizes="(max-width: 880px) 100vw, 880px" />](http://maximumdeveloper.com/wp-content/uploads/2015/03/Screen-Shot-2015-03-08-at-17.14.11.png)

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_18">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fmy-favourite-debugging-technique-code-evaluation%2F&linkname=My%20favourite%20debugging%20technique%20%E2%80%93%20Code%20Evaluation" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fmy-favourite-debugging-technique-code-evaluation%2F&linkname=My%20favourite%20debugging%20technique%20%E2%80%93%20Code%20Evaluation" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fmy-favourite-debugging-technique-code-evaluation%2F&linkname=My%20favourite%20debugging%20technique%20%E2%80%93%20Code%20Evaluation" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>