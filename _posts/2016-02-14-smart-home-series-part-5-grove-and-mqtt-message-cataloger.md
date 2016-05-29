---
id: 585
title: 'Smart home series – Part 5 &#8211; Grove and MQTT-Message-Cataloger'
date: 2016-02-14T20:28:54+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=585
permalink: /smart-home-series-part-5-grove-and-mqtt-message-cataloger/
dsq_thread_id:
  - 4579459260
categories:
  - Uncategorized
tags:
  - IoT
  - Programming
  - Python
  - Raspberry Pi
  - Smart home series
---
Progress is being made on the Smart Home project! I finally got the GrovePi+ with sensors I talked about <a href="http://gjermundbjaanes.com/smart-home-series-part-4-out-with-arduino-in-with-raspberry-pi/" target="_blank">last time.</a>

<!--more-->
It was almost everything I ever wanted. There are a few things that bothers me slightly, but it is not enough to bring my spirits down. I love Grove!

While I was waiting for the Grove stuff to arrive, I started creating a new application I knew I needed in my system: Something to save all the MQTT messages to a database.

&nbsp;

# MQTT-Message-Cataloger

I needed a pretty simple application. Something to listen to MQTT messages on specific topics and save those messages to a database. That way I can have other applications fetch data from said database and use it for stuff (like displaying statistics and other things, Im sure).

The application is written in Python and is thought to run on a Raspberry Pi (of course - where else!?). It uses a config file to set up connections to the MQTT broker and a Mongo Database. You give it a list of topics to listen for, and just let it loose.

&nbsp;

The code is available at Github:

<a href="https://github.com/bjaanes/mqtt-message-cataloger" target="_blank">https://github.com/bjaanes/mqtt-message-cataloger</a>

&nbsp;

# Grove

Let's just start out with what I didn't like about the Grove stuff: The documentation isn't always 100%. The language is sometimes a bit lacking, and it seems outdated some places. It works, and you usually don't have to mess too much around to make things work - but it's not perfect.

However, it DOES work. And it was so nice to have software problems, instead of hardware ones. I can understand software issues - those are easily debuggable. It was heaven compared to the Ardunio mess.

&nbsp;

&nbsp;

## Setup

To install the needed software and prepare you Raspberry for the Grove, just follow this guide:
  
http://www.seeedstudio.com/wiki/GrovePi%2B#Get_Started

Testing it with a sample project (based on which sensor you got).

I tested with the Temperature sensor:
  
<a href="http://www.seeedstudio.com/depot/Grove-Temperature-Sensor-p-774.html" target="_blank">http://www.seeedstudio.com/depot/Grove-Temperature-Sensor-p-774.html</a>

Using the following instructions:
  
<a href="http://www.seeedstudio.com/wiki/index.php?title=Grove_-_Temperature_Sensor&uselang=en#With_Raspberry_Pi" target="_blank">http://www.seeedstudio.com/wiki/index.php?title=Grove_-_Temperature_Sensor&uselang=en#With_Raspberry_Pi</a>

The instructions said to plug it into D3, but I found that the code used A0... That's OK, just plug it in A0 instead.

&nbsp;

## Trying it for real

The next step was to create a "real" test application with all of this. So I created a small application to read the temperature and publish it to the MQTT broker.

First I had to install the Grove libraries globally like so:

Inside Software/Python (This is inside the folder downloaded in the setup guide):

<pre class="lang:sh decode:true ">sudo python setup.py install</pre>

&nbsp;

I could then create a script like this:

&nbsp;

<pre class="lang:python decode:true ">#!/usr/bin/env python

import paho.mqtt.publish as publish
import grovepi
import time

sensor = 0

def readTemperature():
    while True:
        try:
            temperature = grovepi.temp(sensor, '1,2')
            publish.single("office/temperature", '{0:0.1f}'.format(temperature), hostname="192.168.10.200")
            time.sleep(2)
        except KeyboardInterrupt:
            break
        except IOError:
            print "IOError happened"

readTemperature()</pre>

&nbsp;

Woho! It works!

I have now ordered more Grove components and more Raspberry Pi's. More is coming soon!

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_61">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-5-grove-and-mqtt-message-cataloger%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%205%20%E2%80%93%20Grove%20and%20MQTT-Message-Cataloger" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-5-grove-and-mqtt-message-cataloger%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%205%20%E2%80%93%20Grove%20and%20MQTT-Message-Cataloger" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-5-grove-and-mqtt-message-cataloger%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%205%20%E2%80%93%20Grove%20and%20MQTT-Message-Cataloger" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>