---
id: 327
title: How to add a newer version of moment.js to Parse Cloud Code
date: 2015-07-19T18:05:52+00:00
author: Gjermund Bjaanes
layout: post
guid: http://maximumdeveloper.com/?p=327
permalink: /how-to-add-a-newer-version-of-moment-js-to-parse-cloud-code/
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
  - 3962788121
suevafree_template:
  - right-sidebar
categories:
  - Uncategorized
tags:
  - Javascript
  - Programming
---
This post will be a short but sweet post I wish I had read last week.

&nbsp;

The Backend-As-A-Service &#8216;Parse&#8217; has a great feature called Cloud Code. It is Javascript that you host and run on Parse&#8217;s infrastructure. You can call it from your apps (via SDK&#8217;s or REST API&#8217;s). It&#8217;s a great way to reuse a lot of code (if you for instance are writing apps for web, iOS and Android &#8211; much of the complex logic can be extracted into Cloud Code).

Anyways, I am currently writing a lot of Cloud Code for my new web app &#8220;Extreme Results&#8221; (which I wrote a little about here: <a href="http://maximumdeveloper.com/learning-web-dev-series-part-5-extreme-results/" target="_blank">Learning Web Dev Series – Part 5: Extreme Results</a>).

&nbsp;

I found myself needing to use moment.js with Cloud Code to have a good way to get the start and end a week for a given date.

Moment.js has great manipulation methods for just this (moment().startOf(&#8216;isoWeek&#8217;)), but unfortunately the built in version in Parse does not support those specific methods (Parse has version 1.7, and for this I needed >2.2).

&nbsp;

The fix for this is super simple!

  1. Download the newest version of moment.js (<a href="http://momentjs.com/" target="_blank">http://momentjs.com/</a>)
  2. Drop it in your cloud folder (the same place where you put you Cloud Code)
  3. Deploy the cloud code (aka. upload the files).
  4. Import your own version of moment.js using: <pre class="lang:js decode:true">var moment = require('cloud/moment');</pre>

&nbsp;

Easy as that!

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_37">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-to-add-a-newer-version-of-moment-js-to-parse-cloud-code%2F&linkname=How%20to%20add%20a%20newer%20version%20of%20moment.js%20to%20Parse%20Cloud%20Code" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-to-add-a-newer-version-of-moment-js-to-parse-cloud-code%2F&linkname=How%20to%20add%20a%20newer%20version%20of%20moment.js%20to%20Parse%20Cloud%20Code" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-to-add-a-newer-version-of-moment-js-to-parse-cloud-code%2F&linkname=How%20to%20add%20a%20newer%20version%20of%20moment.js%20to%20Parse%20Cloud%20Code" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>