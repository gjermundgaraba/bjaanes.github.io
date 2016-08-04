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
I have set up a couple Raspberry Pi's with GrovePi+ and a few sensors. They send out data with MQTT.

That is not so useful without something to pick up those MQTT messages and doing something about them. Like showing them to me...

<!--more-->
&nbsp;

I mentioned [last time]({{ site.baseurl}}/smart-home-series-part-5-grove-and-mqtt-message-cataloger/){:target="_blank"} that I created a MQTT-message-cataloger that would save all these values to a database. The plan _was_ to pick to values up from something else and show them in some sort of dashboard.

I have changed my mind. There is a great existing tool that seems to fit all my needs: OpenHAB.

&nbsp;

# OpenHAB


![OpenHab Logo]({{ site.baseurl}}/wp-content/uploads/2016/04/openhab-logo.png)

&nbsp;

OpenHAB, in their own words is "a vendor and technology agnostic open source automation software for your home"

It's basically a very powerful home automation hub that works with a bunch of different types of technologies.

&nbsp;

I have been using part of my Easter vacation playing with OpenHAB, and it seems to work very well.

It's not the easiest to set up, because you have to fiddle with a bunch of configuration files. But it works, and it seems to be able to do everything I need it to (right now at least).

It can show real time data from MQTT (and a ton of other protocols), and it supports a bunch of different options for persistence.

&nbsp;

You can read more about OpenHAB on their website:

[http://www.openhab.org/](http://www.openhab.org/){:target="_blank"}

&nbsp;

# The Setup

I have currently 3 Raspberry Pi's working for me. I have one with OpenHAB and the MQTT message broker and two others placed in my apartment with some sensors attached to them.

![Raspberry Pi with Grove]({{ site.baseurl}}/wp-content/uploads/2016/04/IMG_20160410_185710.jpg)

&nbsp;

It's not pretty yet, but I have bought some super generic electronic project boxes from ebay to put them in.

It will look nice at some point, I promise!

&nbsp;

The OpenHAB setup exists of two rooms with some real time data from the sensors there. All using MQTT messages.

In the OpenHAB app, it looks like this:

&nbsp;

![OpenHAB Screenshot Home]({{ site.baseurl}}/wp-content/uploads/2016/04/Screenshot_20160410-143816.png)

![OpenHAB Screenshot Office]({{ site.baseurl}}/wp-content/uploads/2016/04/Screenshot_20160410-143834.png)

![OpenHAB Screenshot Living Room]({{ site.baseurl}}/wp-content/uploads/2016/04/Screenshot_20160410-143850.png)

&nbsp;

It's not much yet - but it's a start!

&nbsp;

# Configuration

It's not the easiest thing to do, since all the setup is done in configuration files. Luckily there exists a bunch of great documentation on the web.

My strategy for learning the configuration was to download the demo site and just changing the configuration to fit my data.

The demo site can be found at their downloads page: 

[http://www.openhab.org/getting-started/downloads.html](http://www.openhab.org/getting-started/downloads.html){:target="_blank"}

&nbsp;

To be able to use MQTT, you have to install an addon for it, and set up the broker. There's a lot of fiddling around basically.

I won't go into detail about exactly how to do all of this here, but an upcoming post I am working on will do just that.

&nbsp;

# Next

I feel like I have a solid starting point for adding more stuff to my smart home.

Except for the fact that it's not really a smart home just yet. It's just a home with some data I can look at. In real time.

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