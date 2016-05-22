---
id: 541
title: 'Smart home series – Part 4 &#8211; Out with Arduino, in with Raspberry Pi'
date: 2016-01-24T16:34:04+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=541
permalink: /smart-home-series-part-4-out-with-arduino-in-with-raspberry-pi/
suevafree_template:
  - right-sidebar
dsq_thread_id:
  - 4519147848
categories:
  - Uncategorized
tags:
  - IoT
  - Raspberry Pi
  - Smart home series
---
After [last posts](http://gjermundbjaanes.com/smart-home-series-part-3-getting-some-momentum/) success of finally getting Arduino to connect to a network, things suddenly started to malfunction again.

Nothing works. Again. And I have no clue why. And I am tired of things just breaking, and not being able to figure out why.

It might be that I am just totally incompetent with Arduino, or that my hardware is just broken. Either way, nothing works.

&nbsp;

# Arduino is out

So I decided that I wanted something I could more easily debug and understand &#8211; a proper computer with less complicated hardware fiddeling to worry about.

Enters Raspberry Pi.

&nbsp;

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/01/rpi1bplus.png" rel="attachment wp-att-543"><img class="wp-image-543 alignnone" src="http://gjermundbjaanes.com/wp-content/uploads/2016/01/rpi1bplus.png" alt="Raspberry Pi Model B+" width="475" height="297" srcset="http://gjermundbjaanes.com/wp-content/uploads/2016/01/rpi1bplus.png 1560w, http://gjermundbjaanes.com/wp-content/uploads/2016/01/rpi1bplus-768x480.png 768w" sizes="(max-width: 475px) 100vw, 475px" /></a>

&nbsp;

The greatest thing about Raspberry Pi, from my point of view, is that it runs Linux and is MADE to connect to networks.

Also, I can understand Linux; I use it every day at work and home.

It got Ethernet built in! And getting WiFi is as easy as plugging in a WiFi USB dongle.

I will of course still need to plug in sensors and whatnot, and for that, I found a solution that looks really nice: Grove System.

&nbsp;

# Grove purchase

Grove is a modular system with ready-to-use sensors and things you can just plug into your system.

All you need is a connector/interface for your system, which you plug all your Grove sensors into.

They have connectors for Arduino (which I didn&#8217;t buy), Raspberry Pi (which I did buy), Beagle Board and many others.

They have all kinds of sensors you can connect and work with, and it looks like there is very little stupid tinkering of hardware that needs to be done &#8211; which fits me right now.

To get started, I ordered:

  * <a href="http://www.seeedstudio.com/depot/GrovePi-p-2241.html" target="_blank">GrovePi+</a>
  * <a href="http://www.seeedstudio.com/depot/Grove-Light-Sensor-p-746.html" target="_blank">Light Sensor</a>
  * <a href="http://www.seeedstudio.com/depot/Grove-Sound-Sensor-p-752.html" target="_blank">Sound Sensor</a>
  * <a href="http://www.seeedstudio.com/depot/Grove-Temperature-Sensor-p-774.html" target="_blank">Temperature Sensor</a>

I plan to buy many others, if this pans out.

&nbsp;

<div id="attachment_542" style="width: 321px" class="wp-caption alignnone">
  <a href="http://gjermundbjaanes.com/wp-content/uploads/2016/01/GrovePi.jpg" rel="attachment wp-att-542"><img class="wp-image-542" src="http://gjermundbjaanes.com/wp-content/uploads/2016/01/GrovePi.jpg" alt="GrovePi+" width="311" height="233" /></a>
  
  <p class="wp-caption-text">
    GrovePi+ The Grove connector to Raspberry Pi.
  </p>
</div>

&nbsp;

They have not yet arrived, but I will write about my experience with Grove when it gets here (in 15-45 days&#8230;).

&nbsp;

# Trying out the Raspberry Pi with a sensor

If you don&#8217;t know what MQTT is, I suggest that you go back and read: <a href="http://gjermundbjaanes.com/smart-home-series-part-1-learning-mqtt-and-buying-stuff/" target="_blank">Smart home series – Part 1 – Learning MQTT and buying stuff</a>

I wanted to prove that getting things to work would be easier with Raspberry Pi, than it was with Arduino. Even without Grove. Just switch out the Arduino for a Raspberry Pi.

I actually got a Raspberry Pi hooked up to a DHT22 (temperature sensor) with just a couple of wires and few lines of code.

It took me a couple of hours to get everything to work (compared to weeks with Arduino &#8211; which never _actually_ worked).

It is even sending MQTT messages to my MQTT broker.

It is an actually  working component! Huzzah! I was SO happy when I saw something finally working like I wanted it to.

&nbsp;

## Hardware

The hardware used:

  * Raspberry Pi Model B+ (with memory card, power, keyboard, monitor and cables)
  * DHT22 sensor
  * Breadboard
  * 10K Resistor
  * A few wires to connect everything

Most of this stuff is dirt cheap. The only thing that has a significant cost is the Raspberry, which is still pretty low-cost.

&nbsp;

## Set up

The first thing I did was to install and set up the Raspberry Pi with a simple Raspbian Jessie Lite image, downloaded from here: <a href="https://www.raspberrypi.org/downloads/raspbian/" target="_blank">https://www.raspberrypi.org/downloads/raspbian/</a>

You don&#8217;t have to use the Lite image if you want a Desktop with GUI and stuff, but I didn&#8217;t really feel like I needed it for this.

&nbsp;

## Connections

To hook up the DHT22 to my Raspberry Pi, I just followed the simple wiring explained in this video:

&nbsp;

<div class="embed-container">
  <span class="embed-youtube" style="text-align:center; display: block;"></span>
</div>

&nbsp;

I am not going to get into the wiring and whatnot, because it is not something I understand completely. It is not a solution I am going to keep either, because I want simpler connections than this (using Grove).

I can show how it ended up looking:

&nbsp;

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/01/1.jpeg" rel="attachment wp-att-544"><img class="alignnone wp-image-544" src="http://gjermundbjaanes.com/wp-content/uploads/2016/01/1.jpeg" alt="Raspberry Pi connection with DHT22" width="443" height="443" srcset="http://gjermundbjaanes.com/wp-content/uploads/2016/01/1.jpeg 893w, http://gjermundbjaanes.com/wp-content/uploads/2016/01/1-150x150.jpeg 150w, http://gjermundbjaanes.com/wp-content/uploads/2016/01/1-768x768.jpeg 768w" sizes="(max-width: 443px) 100vw, 443px" /></a>

Not very pretty, I know.

&nbsp;

## The Code

Now we are getting somewhere comfortable!

I wrote a python script to send an MQTT message every 30 second with the current temperature read-out.

I am using two libraries to do this:

  * Adafruit DHT (mentioned in the Youtube video): <a href="https://github.com/adafruit/Adafruit_Python_DHT" target="_blank">https://github.com/adafruit/Adafruit_Python_DHT</a>
  * Paho MQTT: <a href="https://pypi.python.org/pypi/paho-mqtt/1.1" target="_blank">https://pypi.python.org/pypi/paho-mqtt/1.1</a>

&nbsp;

Adafruit DHT is used to communicate with the DHT22 (temperature sensor) and Paho MQTT is used to publish MQTT messages.

&nbsp;

The logic is very simple:

In an infinite loop I do the following:

  1. Read the temperature (and humidity actually, but I am currently not using it)
  2. Publish the temperature to &#8220;office/temperature&#8221; (which is the MQTT subject I decided would be appropriate)
  3. Sleep for 30 seconds

And so it goes, forever.

&nbsp;

<pre class="lang:python decode:true">#!/usr/bin/env python

import Adafruit_DHT as dht
import paho.mqtt.publish as publish
import time

def readTemperature():
    while True:
        h, t = dht.read_retry(dht.DHT22, 4) #4 is the GPIO number I am connected to on the Raspberry Pi
        publish.single("office/temperature", '{0:0.1f}'.format(t), hostname="192.168.10.200")
        time.sleep(30)

readTemperature()</pre>

I have to admit, I don&#8217;t have much experience with Python yet, so the above code might be very inefficient and ugly &#8211; but it works!

The only issue I have, is that I have to start the script as root. It&#8217;s because the Adafruit library requires root access to read out from the pins on the Raspberry Pi. I am not focusing on that, but I don&#8217;t want that in the future, if I can avoid it.

&nbsp;

So to run the script I just write the following in the terminal:

<pre class="lang:sh decode:true ">sudo python temperature.py</pre>

&nbsp;

&nbsp;

## Does everything work?

I have a MQTT client on my computer called MQTTfx, which I use to test the other clients and the broker. I just subscribe to &#8220;office/temperature&#8221; from my broker, and I can see the temperature getting published every 30 seconds.

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/01/MQTTfx.png" rel="attachment wp-att-547"><img class="alignnone wp-image-547" src="http://gjermundbjaanes.com/wp-content/uploads/2016/01/MQTTfx.png" alt="MQTTfx - MQTT client" width="668" height="501" srcset="http://gjermundbjaanes.com/wp-content/uploads/2016/01/MQTTfx.png 1026w, http://gjermundbjaanes.com/wp-content/uploads/2016/01/MQTTfx-768x576.png 768w" sizes="(max-width: 668px) 100vw, 668px" /></a>

Nice! Things that work, feels great after struggeling for such a long time with Arduino. This was much more fun!

&nbsp;

# Next

While waiting for the Grove components to get here, I am probably going to play around with the hardware I got, and learn a little bit more Python.

I might also get started on an application to pick up MQTT messages and do something useful with them. Perhaps store them away in some database. And possibly show them on a monitor &#8211; which might require a web interface of some kind.

&nbsp;

I don&#8217;t really know how things will look later, but that is half the fun.

Just learning about the possibilities and experimenting/playing with them was one of the reasons I started this project in the first place.

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_58">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-4-out-with-arduino-in-with-raspberry-pi%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%204%20%E2%80%93%20Out%20with%20Arduino%2C%20in%20with%20Raspberry%20Pi" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-4-out-with-arduino-in-with-raspberry-pi%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%204%20%E2%80%93%20Out%20with%20Arduino%2C%20in%20with%20Raspberry%20Pi" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-4-out-with-arduino-in-with-raspberry-pi%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%204%20%E2%80%93%20Out%20with%20Arduino%2C%20in%20with%20Raspberry%20Pi" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>