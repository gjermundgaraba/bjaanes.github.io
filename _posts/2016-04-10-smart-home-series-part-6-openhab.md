---
id: 662
title: Smart home series – Part 6 – OpenHAB
date: 2016-04-10T18:10:36+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=662
permalink: /smart-home-series-part-6-openhab/
dsq_thread_id:
  - 4737270360
categories:
  - Uncategorized
tags:
  - IoT
  - Raspberry Pi
  - Smart home series
---
I have set up a couple Raspberry Pi&#8217;s with GrovePi+ and a few sensors. They send out data with MQTT.

That is not so useful without something to pick up those MQTT messages and doing something about them. Like showing them to me&#8230;

<!--more-->
&nbsp;

I mentioned <a href="http://gjermundbjaanes.com/smart-home-series-part-5-grove-and-mqtt-message-cataloger/" target="_blank">last time</a> that I created a MQTT-message-cataloger that would save all these values to a database. The plan _was_ to pick to values up from something else and show them in some sort of dashboard.

I have changed my mind. There is a great existing tool that seems to fit all my needs: OpenHAB.

&nbsp;

# OpenHAB

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/04/openhab-logo.png" rel="attachment wp-att-663"><img class="alignnone size-full wp-image-663" src="http://gjermundbjaanes.com/wp-content/uploads/2016/04/openhab-logo.png" alt="OpenHAB Logo" width="285" height="81" /></a>

&nbsp;

OpenHAB, in their own words is &#8220;a vendor and technology agnostic open source automation software for your home&#8221;

It&#8217;s basically a very powerful home automation hub that works with a bunch of different types of technologies.

&nbsp;

I have been using part of my Easter vacation playing with OpenHAB, and it seems to work very well.

It&#8217;s not the easiest to set up, because you have to fiddle with a bunch of configuration files. But it works, and it seems to be able to do everything I need it to (right now at least).

It can show real time data from MQTT (and a ton of other protocols), and it supports a bunch of different options for persistence.

&nbsp;

You can read more about OpenHAB on their website:

<a href="http://www.openhab.org/" target="_blank">http://www.openhab.org/</a>

&nbsp;

# The Setup

I have currently 3 Raspberry Pi&#8217;s working for me. I have one with OpenHAB and the MQTT message broker and two others placed in my apartment with some sensors attached to them.

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/04/IMG_20160410_185710.jpg" rel="attachment wp-att-664"><img class="alignnone wp-image-664" src="http://gjermundbjaanes.com/wp-content/uploads/2016/04/IMG_20160410_185710.jpg" alt="Raspberry Pi with Grove" width="369" height="491" /></a>

&nbsp;

It&#8217;s not pretty yet, but I have bought some super generic electronic project boxes from ebay to put them in.

It will look nice at some point, I promise!

&nbsp;

The OpenHAB setup exists of two rooms with some real time data from the sensors there. All using MQTT messages.

In the OpenHAB app, it looks like this:

&nbsp;

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143816.png" rel="attachment wp-att-665"><img class="alignnone wp-image-665" src="http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143816.png" alt="OpenHAB Screenshot Home" width="271" height="482" srcset="http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143816.png 1080w, http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143816-768x1365.png 768w" sizes="(max-width: 271px) 100vw, 271px" /></a>

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143834.png" rel="attachment wp-att-666"><img class="alignnone wp-image-666" src="http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143834.png" alt="OpenHAB Screenshot Office" width="273" height="485" srcset="http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143834.png 1080w, http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143834-768x1365.png 768w" sizes="(max-width: 273px) 100vw, 273px" /></a>

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143850.png" rel="attachment wp-att-667"><img class="alignnone wp-image-667" src="http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143850.png" alt="OpenHAB Screenshot Living Room" width="272" height="484" srcset="http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143850.png 1080w, http://gjermundbjaanes.com/wp-content/uploads/2016/04/Screenshot_20160410-143850-768x1365.png 768w" sizes="(max-width: 272px) 100vw, 272px" /></a>

&nbsp;

It&#8217;s not much yet &#8211; but it&#8217;s a start!

&nbsp;

# Configuration

It&#8217;s not the easiest thing to do, since all the setup is done in configuration files. Luckily there exists a bunch of great documentation on the web.

My strategy for learning the configuration was to download the demo site and just changing the configuration to fit my data.

The demo site can be found at their downloads page: <a href="http://www.openhab.org/getting-started/downloads.html" target="_blank">http://www.openhab.org/getting-started/downloads.html</a>

&nbsp;

To be able to use MQTT, you have to install an addon for it, and set up the broker. There&#8217;s a lot of fiddling around basically.

I won&#8217;t go into detail about exactly how to do all of this here, but an upcoming post I am working on will do just that.

&nbsp;

# Next

I feel like I have a solid starting point for adding more stuff to my smart home.

Except for the fact that it&#8217;s not really a smart home just yet. It&#8217;s just a home with some data I can look at. In real time.

&nbsp;

I need  bunch of more stuff for this to make any sense. I need to be able to automatically act upon the data I have.

I need to be able to look at statistics over time. I need to be able to control things like heating and lighting automatically and manually.

That is the next step. One simple use case I want to realize is the possibility to turn off ALL the light in apartment from my phone.

&nbsp;

Like I mentioned earlier in the post, there will come a blog post soon with details on how I actually set all this up. A guide of sorts.

If you are interested in that, keep an eye on this blog 🙂

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_69">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-6-openhab%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%206%20%E2%80%93%20OpenHAB" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-6-openhab%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%206%20%E2%80%93%20OpenHAB" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-6-openhab%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%206%20%E2%80%93%20OpenHAB" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>