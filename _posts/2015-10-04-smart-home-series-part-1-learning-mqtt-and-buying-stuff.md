---
id: 393
title: 'Smart home series &#8211; Part 1 &#8211; Learning MQTT and buying stuff'
date: 2015-10-04T19:03:46+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=393
permalink: /smart-home-series-part-1-learning-mqtt-and-buying-stuff/
suevafree_template:
  - right-sidebar
dsq_thread_id:
  - 4193544356
categories:
  - Uncategorized
tags:
  - Arduino
  - IoT
  - Programming
  - Raspberry Pi
  - Smart home series
---
Since [last time](http://gjermundbjaanes.com/smart-home-series-part-0-starting-point/) I have worked a little bit on making some progress with my smart house project. I have been doing some reading, as well as some buying.

<!--more-->
&nbsp;

# MQTT

As far as I have learned, MQTT is the current preferred protocol for doing communication between small embedded devices. I seems simple and covers a lot of the problems that IoT and embedded devices face.

<img class="alignnone size-full wp-image-394" src="http://gjermundbjaanes.com/wp-content/uploads/2015/10/mqttorg-glow.png" alt="MQTT logo" width="260" height="68" />

MQTT is a publish-subscribe messaging protocol that works well with limited network bandwidth, unstable connections and small devices (e.g. Arduino-like devices).

The protocol is based on one or more devices subscribing to “topics” and one or more devices publishing on “topics”. The subscribing devices get all messages for a specific topic that someone publishes on.

You also need a message broker to control the flow of all these messages. It’s like a little master server making sure everyone get their messages. So in reality, every publisher sends a message to the broker, and the broker makes sure every subscriber gets a copy of that message.

[<img class="alignnone wp-image-395" src="http://gjermundbjaanes.com/wp-content/uploads/2015/10/Document_2015-10-04_11-36-38-1-.png" alt="MQTT logo" width="505" height="390" />](http://gjermundbjaanes.com/wp-content/uploads/2015/10/Document_2015-10-04_11-36-38-1-.png)

For instance, let say you have a temperature sensor device publishing on “/temperature/kitchen”. Every minute, the temperature sends out a message on &#8220;/temperature/kitchen&#8221; with the current temperature. The broker gets that messages and sends out two messages to it’s two subscribers. One log server that saves the temperature for historical view and a light bulb that shows a different hue depending on the temperature it receives (e.g. red for hot, blue for cold).

&nbsp;

# My Plan for MQTT

I am planning on using a first-generation Raspberry Pi as my MQTT broker, and Raspberry Pi 2 for a small multipurpose data server (storing, viewing, statistics, etc.).

I will be using Arduino somehow for the sensor devices, but I haven’t figured out how to create small permanent devices with Arduino yet. I&#8217;ll figure that out later!

I highly recommend that you spend some time learning this technology, because it seems to be one of the cornerstones of this particular field. I watched this talk about MQTT, which even have a live demo:

<div class="embed-container">
  <span class="embed-youtube" style="text-align:center; display: block;"></span>
</div>

&nbsp;

# Buying

I have bought a lot of stuff the last weeks. I went absolutely nuts on eBay and few electronic shops. I bought soldering tools, sensors, breadboards, wires, capacitors, resistors, storage boxes and some stuff to try to make my own small permanent Arduino device (we&#8217;ll see how that goes!).

[<img class="alignnone wp-image-397" src="http://gjermundbjaanes.com/wp-content/uploads/2015/10/IMG_0510.jpg" alt="Stuff bought" width="428" height="321" />](http://gjermundbjaanes.com/wp-content/uploads/2015/10/IMG_0510.jpg)

I still don’t know exactly what I truly need, but as soon as I really figure that out, I will let you know. For now I am stumbling around in this new landscape of electronics, IoT and embedded devices.

Until next time!

&nbsp;

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_46">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-1-learning-mqtt-and-buying-stuff%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%201%20%E2%80%93%20Learning%20MQTT%20and%20buying%20stuff" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-1-learning-mqtt-and-buying-stuff%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%201%20%E2%80%93%20Learning%20MQTT%20and%20buying%20stuff" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-1-learning-mqtt-and-buying-stuff%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%201%20%E2%80%93%20Learning%20MQTT%20and%20buying%20stuff" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>