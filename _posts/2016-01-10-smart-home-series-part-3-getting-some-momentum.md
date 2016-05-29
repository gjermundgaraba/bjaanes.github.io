---
id: 536
title: 'Smart home series – Part 3 &#8211; Getting some momentum'
date: 2016-01-10T19:08:14+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=536
permalink: /smart-home-series-part-3-getting-some-momentum/
suevafree_template:
  - right-sidebar
dsq_thread_id:
  - 4479561065
categories:
  - Uncategorized
tags:
  - IoT
  - Smart home series
---
It&#8217;s been a little while since I had any update for my Smart home series.

The last time I thought I had failed miserably at soldering, but after a brand new component gave the same errors, I finally sought some help.

<!--more-->
Turns out I the problem was with my Arduino setup. According to the help I got, the problem was:

_&#8220;When you program the UNO using USB it communicates with the &#8216;328 via pins D0 & D1. The ESP8266 is interfering with this process.&#8221;_

The thread I started to get help: <a href="https://forum.arduino.cc/index.php?topic=369554.0" target="_blank">https://forum.arduino.cc/index.php?topic=369554.0</a>

So the solution to my problem was to have the following code in my sketch:

<pre class="lang:c decode:true">#include &lt;SoftwareSerial.h&gt;
SoftwareSerial MySerial(8, 9);</pre>

I was then finally able to upload and test the shield, which worked like a charm! I managed to connect to my WiFi network and ping a server. Yes!

&nbsp;

# MQTT

Finally, with some momentum, I wanted to set up an MQTT broker and get the basic setup up and running.

I explained the basic principles with MQTT in one of my previous posts: <a href="http://gjermundbjaanes.com/smart-home-series-part-1-learning-mqtt-and-buying-stuff/" target="_blank">Smart home series – Part 1 – Learning MQTT and buying stuff</a>

I have a first generation Raspberry Pi, which I am going to use as my MQTT broker.

I installed a Debian variant called Raspbian Jessie Lite and the MQTT broker software Mosquitto.

The images can be found here: <a href="https://www.raspberrypi.org/downloads/raspbian/" target="_blank">https://www.raspberrypi.org/downloads/raspbian/</a>

I installed Mosquitto using the following commands:

<pre class="lang:sh decode:true ">curl -O http://repo.mosquitto.org/debian/mosquitto-repo.gpg.key
sudo apt-key add mosquitto-repo.gpg.key
rm mosquitto-repo.gpg.key
cd /etc/apt/sources.list.d/
sudo curl -O http://repo.mosquitto.org/debian/mosquitto-jessie.list
sudo apt-get update
sudo apt-get install mosquitto mosquitto-clients</pre>

&nbsp;

To test the setup I installed a basic MQTT client on my normal computer, and connected to the raspberry.

In order to see the incoming messages, I used the following command on the Raspberry server:

<pre class="lang:sh decode:true ">mosquitto_sub -d -t hello/world</pre>

&nbsp;

I then published a message on hello/world.
  
On my raspberry, I could see the following message:

<pre class="lang:sh decode:true ">Client mosqsub/7714-raspberryp received PUBLISH (d0, q0, r0, m0, 'hello/world', ... (0 bytes))</pre>

&nbsp;

Success! The broker is up and running!

&nbsp;

# Next steps

Now that I finally have some momentum I hope to get something useful created pretty soon.

The big next step is obviously to get my Arduino to somehow send MQTT messages based on information from one of my sensors.

After that it&#8217;s all programming, testing and tweaking. Look out for more updates!

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_57">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-3-getting-some-momentum%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%203%20%E2%80%93%20Getting%20some%20momentum" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-3-getting-some-momentum%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%203%20%E2%80%93%20Getting%20some%20momentum" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fsmart-home-series-part-3-getting-some-momentum%2F&linkname=Smart%20home%20series%20%E2%80%93%20Part%203%20%E2%80%93%20Getting%20some%20momentum" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>