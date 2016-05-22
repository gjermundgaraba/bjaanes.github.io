---
id: 671
title: How to set up Raspberry pi with Grove and MQTT
date: 2016-04-24T19:10:00+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=671
permalink: /how-to-set-up-raspberry-pi-with-grove-and-mqtt/
suevafree_template:
  - right-sidebar
dsq_thread_id:
  - 4773285239
categories:
  - Uncategorized
tags:
  - IoT
  - Programming
  - Python
  - Raspberry Pi
---
I have spent some time in my <a href="http://gjermundbjaanes.com/tag/smart-home-series/" target="_blank">Smart Home Series</a> to experiment with different technologies. I found out that Arduino is not the best fit for me and my plans, so I bought some Raspberry Pi&#8217;s and Grove components.

You can read more about my decision around that in this blog post:

[Smart home series – Part 4 – Out with Arduino, in with Raspberry Pi](http://gjermundbjaanes.com/smart-home-series-part-4-out-with-arduino-in-with-raspberry-pi/)

&nbsp;

Grove is a modular system with ready-to-use sensors and things you can just plug into your system (in my case, Raspberry Pi) and program easily against.

That means very little tinkering with hardware, mostly just plug-and-play. Exactly what I wanted.

&nbsp;

&nbsp;

In this post, I will go through the steps I made to set up my Raspberry Pi&#8217;s, and how you can get started creating scripts that does something useful.

&nbsp;

If you are not familiar with MQTT, It might be helpful to read a little about it first here (although certainly not required):

<a href="http://gjermundbjaanes.com/smart-home-series-part-1-learning-mqtt-and-buying-stuff/" target="_blank">Smart home series – Part 1 – Learning MQTT and buying stuff</a>

&nbsp;

The form of the &#8220;guide&#8221; is a mix of what I did, and step by step instructions on how you can do it.

&nbsp;

# Installation and preparation of the Pi

&nbsp;

## OS

First off, I bought the cheapest Pi&#8217;s I could find, which were the first generation B+ model. Therefore I figured I would be best off with a lightweight Linux image.

I chose the Raspbian Jessie Lite image. I downloaded that and installed it on a memory card.

<div class="embed-container">
  <blockquote data-secret="qP6npfFjHY" class="wp-embedded-content">
    <a href="https://www.raspberrypi.org/downloads/raspbian/">Raspbian</a></p>
  </blockquote>
  
  <p>
    </div> 
    
    <p>
      &nbsp;
    </p>
    
    <p>
      If you need some help with the flashing process (which is fairly easy and straightforward), their website is very helpful:
    </p>
    
    <p>
      <a href="https://www.raspberrypi.org/documentation/installation/installing-images/README.md" target="_blank">https://www.raspberrypi.org/documentation/installation/installing-images/README.md</a>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      I then inserted the memory card into the Raspberry Pi and booted it up. Username &#8220;pi&#8221; and password &#8220;raspberry&#8221;. Easy as p.. Nope, not going there!
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Configuration
    </h2>
    
    <p>
      The first thing I had to do was to configure keyboard, timezone, change password and free up storage on the memory card.
    </p>
    
    <p>
      All this is done in the configuration tool called &#8220;raspi-config&#8221;.
    </p>
    
    <p>
      Just run raspi-config from the terminal and use the alternatives to set up everything you might need.
    </p>
    
    <pre class="lang:sh decode:true ">sudo raspi-config</pre>
    
    <p>
      Some of them might be:<br /> 1 Expand Filesystem<br /> 2 Change User Password<br /> 5 Internationalization Options
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Static IP
    </h2>
    
    <p>
      The final general configuration I made was to set up a static IP address. I didn&#8217;t want to run around with monitors and keyboards every time I wanted to change something on the machines. SSH to the rescue!
    </p>
    
    <p>
      And to use SSH, I really prefer a static IP.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      To set up a static IP address, follow these steps:
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Open dhcpd.conf with your favorite linux text editor (mine is vim, but you could use nano or something similar if you&#8217;d like).
    </p>
    
    <pre class="lang:sh decode:true ">sudo nano /etc/dhcpd.conf</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      At the end of the file, add the following (but remember to change the IP addresses to fit you network and needs):
    </p>
    
    <pre class="lang:default decode:true ">static interface eth0
static ip_address=192.168.10.200/24
static routers=192.168.10.1
static domain_name_servers=192.168.10.1</pre>
    
    <p>
      You have to change out the IP addresses so they fit your network &#8211; but it should be fairly straightforward if you have a little network knowledge.
    </p>
    
    <p>
      A tip might be to check the existing values you got from your local DHCP server. To see the existing values, run the following command:
    </p>
    
    <pre class="lang:sh decode:true ">ifconfig</pre>
    
    <p>
      Save the file and reboot.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Run the following command to verify your new IP:
    </p>
    
    <pre class="lang:sh decode:true ">ifconfig</pre>
    
    <p>
      You should see the static IP you set up.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Installing GrovePi+
    </h2>
    
    <p>
      Next up is to install the GrovePi+ files.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      First, install git.
    </p>
    
    <pre class="lang:sh decode:true ">sudo apt-get install git</pre>
    
    <p>
      Then you need to download the GrovePi software:
    </p>
    
    <pre class="lang:sh decode:true ">cd /home/pi
sudo git clone https://github.com/DexterInd/GrovePi</pre>
    
    <p>
      Install it:
    </p>
    
    <pre class="lang:sh decode:true ">cd /home/pi/GrovePi/Script
sudo chmod +x install.sh
sudo ./install.sh</pre>
    
    <p>
      This process takes quite a bit of time. At some point you have to follow some instructions, but the script takes care of the installation for the most part.
    </p>
    
    <p>
      At the end, the script will reboot the Pi, and you have to log in again.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      You are now ready to start using the GrovePi+ Shield &#8211; but first:
    </p>
    
    <p>
      Shut down the pi:
    </p>
    
    <pre class="lang:sh decode:true ">sudo poweroff</pre>
    
    <p>
      Put the GrovePi shield on your Raspberry Pi.
    </p>
    
    <p>
      Power it up again and verify that the installation was successful by running:
    </p>
    
    <pre class="lang:sh decode:true ">sudo i2cdetect -y 1</pre>
    
    <p>
      If you can see a “04” in the output, this means the Raspberry Pi is able to detect the GrovePi.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      The installation is also documented on this site:
    </p>
    
    <div class="embed-container">
      <blockquote data-secret="nZs6z6dJEI" class="wp-embedded-content">
        <a href="http://www.dexterindustries.com/GrovePi/get-started-with-the-grovepi/setting-software/">Setting Up The Software</a></p>
      </blockquote>
      
      <p>
        </div> 
        
        <p>
          &nbsp;
        </p>
        
        <p>
          &nbsp;
        </p>
        
        <h1>
          Installing the GrovePi+ libraries globally
        </h1>
        
        <p>
          I have written all my script in Python, and found that installing the Grove Python libraries globally really helps a lot.
        </p>
        
        <pre class="lang:sh decode:true ">cd /home/pi/GrovePi/Software/Python
sudo python setup.py install</pre>
        
        <p>
          I wanted to use MQTT to send sensor data from the Pi&#8217;s, so I needed a Python library that would let me do that.
        </p>
        
        <p>
          paho-mqtt was that library. There are several ways to install it, but I found the most straightforward way was to download the code with git and install it manually.
        </p>
        
        <pre class="lang:sh decode:true ">cd /home/pi
git clone git://git.eclipse.org/gitroot/paho/org.eclipse.paho.mqtt.python.git
cd org.eclipse.paho.mqtt.python
sudo python setup.py install</pre>
        
        <p>
          The website for paho-mqtt can be found here:
        </p>
        
        <p>
          <a href="https://pypi.python.org/pypi/paho-mqtt/1.1" target="_blank">https://pypi.python.org/pypi/paho-mqtt/1.1</a>
        </p>
        
        <p>
          &nbsp;
        </p>
        
        <h1>
          Actually reading data with Grove
        </h1>
        
        <p>
          Exactly how to read the data depends very much on the sensors you have, but I will use the normal Temperature sensor as an example.
        </p>
        
        <p>
          The great thing is that in the GrovePi folder, you have access to examples for most of the sensors. They are very helpful!<br /> They can be found in the following location:
        </p>
        
        <p>
          /home/pi/GrovePi/Software/Python
        </p>
        
        <p>
          &nbsp;
        </p>
        
        <p>
          All you have to do is make sure the sensor port number is correct (just look at the example script for your sensor, and you should get a clue to what you can do).
        </p>
        
        <p>
          For instance, if you have purchased the Grove temperature sensor, there is an example script called grove_temperature_sensor.py
        </p>
        
        <p>
          The code looks like this:
        </p>
        
        <pre class="lang:python decode:true">import time
import grovepi

# Connect the Grove Temperature Sensor to analog port A0
# SIG,NC,VCC,GND
sensor = 0

while True:
  try:
    temp = grovepi.temp(sensor, '1.1')
    print ("temp =", temp)
    time.sleep(.5)

  except KeyboardInterrupt:
    break
  except IOError:
    print ("Error")</pre>
        
        <p>
          It is fairly simple. It reads the temperature every 0.5 seconds and prints it out. The important thing to note here is the sensor variable at the top of the script.
        </p>
        
        <p>
          That is the analog port A0 it points to.
        </p>
        
        <p>
          To test out your temperature sensor, you would insert the sensor in the Analog 0 port, and run the scrip with something like
        </p>
        
        <pre class="lang:sh decode:true ">sudo python ./grove_temperature_sensor.py</pre>
        
        <p>
          &nbsp;
        </p>
        
        <h1>
          Your very own script using Grove
        </h1>
        
        <p>
          You&#8217;d might like your sensor data to be sent somewhere (and not just printed out in the terminal window).
        </p>
        
        <p>
          What I did was to publish the sensor data with MQTT.
        </p>
        
        <p>
          A typical script I have written lately might look like this:
        </p>
        
        <pre class="lang:python decode:true">#!/usr/bin/env python

import paho.mqtt.publish as publish
import grovepi
import time

temp_sensor = 0

def readTemperature():
  while True:
    try:
      temperature = grovepi.temp(temp_sensor, '1,2')
      publish.single("office/temperature", '{0:0.1f}'.format(temperature), hostname="192.168.10.200")
      time.sleep(5)
    except KeyboardInterrupt:
      break
    except IOError:
      print "IOError happened"

readTemperature()</pre>
        
        <p>
          The basic concept is simple:
        </p>
        
        <p>
          Every 5 seconds, read the temperature and publish it to the MQTT broker, on 192.168.10.200, with the topic &#8220;office/temperature&#8221;.
        </p>
        
        <p>
          If I have more than one sensor I just read and publish the data one at the time inside the try block.
        </p>
        
        <p>
          &nbsp;
        </p>
        
        <p>
          The important thing to notice here is that most of the work is done by the libraries I import. More specifically, the grovepi library, and the mqtt library (the publishing part of it).
        </p>
        
        <p>
          &nbsp;
        </p>
        
        <h1>
          Making the script run on startup
        </h1>
        
        <p>
          Once you have created a python script you want to run without interference (when you log out, restart or do whatever, you still want this script to run).
        </p>
        
        <p>
          I have done this using something called upstart. I&#8217;ll show you how to set that up properly.
        </p>
        
        <p>
          &nbsp;
        </p>
        
        <p>
          First, install upstart:
        </p>
        
        <pre class="lang:sh decode:true ">sudo apt-get install upstart</pre>
        
        <p>
          Then, you have to create an init configuration for your script.
        </p>
        
        <pre class="lang:sh decode:true ">sudo nano /etc/init/sensors.conf</pre>
        
        <pre class="lang:default decode:true">start on runlevel [2345]
stop on runlevel [016]

respawn
exec python /home/pi/code/sensors.py</pre>
        
        <p>
          Just remember to change the path to your python script.
        </p>
        
        <p>
          &nbsp;
        </p>
        
        <p>
          This will make the sensors.py script run on startup, and if it ever crashes, it will restart by itself.
        </p>
        
        <p>
          Reboot, and your script should run after startup.
        </p>
        
        <p>
          To verify that your script is running:
        </p>
        
        <pre class="lang:sh decode:true ">ps aux | grep sensors.py</pre>
        
        <p>
          You should see something like this:
        </p>
        
        <pre class="lang:default decode:true ">root 7157 0.7 2.0 11348 8936 ? Ss 03:59 3:38 python /home/pi/code/sensors.py</pre>
        
        <p>
          You should also check with a MQTT client that your messages can be listened to.
        </p>
        
        <p>
          &nbsp;
        </p>
        
        <p>
          Now that you have a Raspberry Pi publishing sensor data, all you have to do is consume that data somehow. For instance with OpenHAB or some other home automation hub.
        </p>
        
        <p>
          I hope this guide helped a bit with getting started with Raspberry Pi and Grove.
        </p>
        
        <div class="addtoany_share_save_container addtoany_content_bottom">
          <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_70">
            <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-to-set-up-raspberry-pi-with-grove-and-mqtt%2F&linkname=How%20to%20set%20up%20Raspberry%20pi%20with%20Grove%20and%20MQTT" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-to-set-up-raspberry-pi-with-grove-and-mqtt%2F&linkname=How%20to%20set%20up%20Raspberry%20pi%20with%20Grove%20and%20MQTT" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-to-set-up-raspberry-pi-with-grove-and-mqtt%2F&linkname=How%20to%20set%20up%20Raspberry%20pi%20with%20Grove%20and%20MQTT" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
          </div>
        </div>