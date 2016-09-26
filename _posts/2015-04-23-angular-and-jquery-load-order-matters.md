---
id: 240
title: Angular and jQuery load order matters!
date: 2015-04-23T07:58:04+00:00
author: Gjermund Bjaanes
layout: post
permalink: /angular-and-jquery-load-order-matters/
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
  - 3705544526
categories:
  - CodeProject
  - Uncategorized
tags:
  - Angular
  - Programming
  - Web
---
While trying to load a jQuery library called zTree into a directive, I came over this weird error:

<pre class="lang:default highlight:0 decode:true ">jqLite#on() does not support the `selector` or `eventData` parameters</pre>

<!--more-->
[<img class="alignnone size-full wp-image-241" src="http://gjermundbjaanes.com/wp-content/uploads/2015/04/D23BBB2D-E0DF-4D32-B6D6-B88ACCA4B081.png" alt="Angular jqLite error on" width="837" height="157" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/04/D23BBB2D-E0DF-4D32-B6D6-B88ACCA4B081.png 837w, http://gjermundbjaanes.com/wp-content/uploads/2015/04/D23BBB2D-E0DF-4D32-B6D6-B88ACCA4B081-300x56.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/04/D23BBB2D-E0DF-4D32-B6D6-B88ACCA4B081-600x113.png 600w" sizes="(max-width: 837px) 100vw, 837px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/04/D23BBB2D-E0DF-4D32-B6D6-B88ACCA4B081.png)

It doesn’t really say that much, but from a little Google’ing I understood that Angular has implemented a subset of jQuery called jqLite which is fairly limited. Loading my particular library was not working with jqLite. Angular is however not supposed to use jqLite when jQuery is available.

<div>
  <pre class="lang:default decode:true">&lt;script src="/angular/angular.js"&gt;&lt;/script&gt;
&lt;script src="/jquery/dist/jquery.js"&gt;&lt;/script&gt;</pre>
</div>

I had loaded jQuery, so why did Angular not use it?
  
The answer to that is the order of the imports. In order for Angular to recognize and use jQuery it has to be loaded before angular gets loaded.

Switching the order solved the issue.

<pre class="lang:default decode:true">&lt;script src="/jquery/dist/jquery.js"&gt;&lt;/script&gt;
&lt;script src="/angular/angular.js"&gt;&lt;/script&gt;</pre>

&nbsp;

So, if you need jQuery, remember load it before Angular.

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_25">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fangular-and-jquery-load-order-matters%2F&linkname=Angular%20and%20jQuery%20load%20order%20matters%21" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fangular-and-jquery-load-order-matters%2F&linkname=Angular%20and%20jQuery%20load%20order%20matters%21" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fangular-and-jquery-load-order-matters%2F&linkname=Angular%20and%20jQuery%20load%20order%20matters%21" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>