---
id: 671
title: How to set up Raspberry pi with Grove and MQTT
date: 2016-04-24T19:10:00+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=671
permalink: /how-to-set-up-raspberry-pi-with-grove-and-mqtt/
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
I have spent some time in my <a href="http://gjermundbjaanes.com/tag/smart-home-series/" target="_blank">Smart Home Series</a> to experiment with different technologies. I found out that Arduino is not the best fit for me and my plans, so I bought some Raspberry Pi's and Grove components.

<!--more-->
You can read more about my decision around that in this blog post:

[Smart home series – Part 4 – Out with Arduino, in with Raspberry Pi](http://gjermundbjaanes.com/smart-home-series-part-4-out-with-arduino-in-with-raspberry-pi/)

&nbsp;

Grove is a modular system with ready-to-use sensors and things you can just plug into your system (in my case, Raspberry Pi) and program easily against.

That means very little tinkering with hardware, mostly just plug-and-play. Exactly what I wanted.

&nbsp;

In this post, I will go through the steps I made to set up my Raspberry Pi's, and how you can get started creating scripts that does something useful.

&nbsp;

If you are not familiar with MQTT, It might be helpful to read a little about it first here (although certainly not required):

[Smart home series – Part 1 – Learning MQTT and buying stuff]({{ site.baseurl }}/smart-home-series-part-1-learning-mqtt-and-buying-stuff/){:target="_blank"} 

The form of the "guide" is a mix of what I did, and step by step instructions on how you can do it yourself.

&nbsp;

# Installation and preparation of the Pi

&nbsp;

## OS

First off, I bought the cheapest Pi's I could find, which were the first generation B+ model. Therefore I figured I would be best off with a lightweight Linux image.

I chose the [Raspbian Jessie Lite image](https://www.raspberrypi.org/downloads/raspbian/){:target="_blank"}. I downloaded that and installed it on a memory card.

If you need some help with the flashing process (which is fairly easy and straightforward), their website is very helpful:

    
<a href="https://www.raspberrypi.org/documentation/installation/installing-images/README.md" target="_blank">https://www.raspberrypi.org/documentation/installation/installing-images/README.md</a>

I then inserted the memory card into the Raspberry Pi and booted it up. Username "pi" and password "raspberry". Easy as pie!

## Configuration

The first thing I had to do was to configure keyboard, timezone, change password and free up storage on the memory card.

All this is done in the configuration tool called "raspi-config".

Just run raspi-config from the terminal and use the alternatives to set up everything you might need.

<pre class="lang:sh decode:true ">
sudo raspi-config
</pre>

Some of them might be:<br /> 1 Expand Filesystem<br /> 2 Change User Password<br /> 5 Internationalization Options

&nbsp;

## Static IP
    
The final general configuration I made was to set up a static IP address. I didn't want to run around with monitors and keyboards every time I wanted to change something on the machines. SSH to the rescue!

And to use SSH, I really prefer a static IP.

&nbsp;

To set up a static IP address, follow these steps:

&nbsp;

Open dhcpd.conf with your favorite linux text editor (mine is vim, but you could use nano or something similar if you'd like).

<pre class="lang:sh decode:true ">
sudo nano /etc/dhcpd.conf
</pre>

&nbsp;

At the end of the file, add the following (but remember to change the IP addresses to fit you network and needs):

<pre class="lang:default decode:true ">
static interface eth0
static ip_address=192.168.10.200/24
static routers=192.168.10.1
static domain_name_servers=192.168.10.1
</pre>

You have to change out the IP addresses so they fit your network - but it should be fairly straightforward if you have a little network knowledge.

A tip might be to check the existing values you got from your local DHCP server. To see the existing values, run the following command:

<pre class="lang:sh decode:true ">
ifconfig
</pre>

Save the file and reboot.

&nbsp;

Run the following command to verify your new IP:

<pre class="lang:sh decode:true ">
ifconfig
</pre>

You should see the static IP you set up.

&nbsp;

##  Installing GrovePi+

Next up is to install the GrovePi+ files.

&nbsp;

First, install git.

<pre class="lang:sh decode:true ">sudo apt-get install git</pre>

Then you need to download the GrovePi software:

<pre class="lang:sh decode:true ">
cd /home/pi
sudo git clone https://github.com/DexterInd/GrovePi
</pre>

Install it:

<pre class="lang:sh decode:true ">
cd /home/pi/GrovePi/Script
sudo chmod +x install.sh
sudo ./install.sh
</pre>

This process takes quite a bit of time. At some point you have to follow some instructions, but the script takes care of the installation for the most part.

At the end, the script will reboot the Pi, and you have to log in again.

&nbsp;

You are now ready to start using the GrovePi+ Shield - but first:

Shut down the pi:

<pre class="lang:sh decode:true ">
sudo poweroff
</pre>

Put the GrovePi shield on your Raspberry Pi.

Power it up again and verify that the installation was successful by running:

<pre class="lang:sh decode:true ">
sudo i2cdetect -y 1
</pre>

If you can see a “04” in the output, this means the Raspberry Pi is able to detect the GrovePi.

&nbsp;

The installation is also documented on this site:

[Setting Up The Software](http://www.dexterindustries.com/GrovePi/get-started-with-the-grovepi/setting-software/){:target="_blank"} 

&nbsp;

#  Installing the GrovePi+ libraries globally

I have written all my script in Python, and found that installing the Grove Python libraries globally really helps a lot.

<pre class="lang:sh decode:true ">
cd /home/pi/GrovePi/Software/Python
sudo python setup.py install
</pre>

I wanted to use MQTT to send sensor data from the Pi's, so I needed a Python library that would let me do that.

paho-mqtt was that library. There are several ways to install it, but I found the most straightforward way was to download the code with git and install it manually.

<pre class="lang:sh decode:true ">
cd /home/pi
git clone git://git.eclipse.org/gitroot/paho/org.eclipse.paho.mqtt.python.git
cd org.eclipse.paho.mqtt.python
sudo python setup.py install
</pre>

The website for paho-mqtt can be found here:

[https://pypi.python.org/pypi/paho-mqtt/1.1](https://pypi.python.org/pypi/paho-mqtt/1.1){:target="_blank"} 

&nbsp;

#  Actually reading data with Grove

Exactly how to read the data depends very much on the sensors you have, but I will use the normal Temperature sensor as an example.

The great thing is that in the GrovePi folder, you have access to examples for most of the sensors. They are very helpful!<br /> They can be found in the following location:

/home/pi/GrovePi/Software/Python

&nbsp;

All you have to do is make sure the sensor port number is correct (just look at the example script for your sensor, and you should get a clue to what you can do).

For instance, if you have purchased the Grove temperature sensor, there is an example script called grove_temperature_sensor.py

The code looks like this:

<pre class="lang:python decode:true">
import time
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
print ("Error")
</pre>

It is fairly simple. It reads the temperature every 0.5 seconds and prints it out. The important thing to note here is the sensor variable at the top of the script.

That is the analog port A0 it points to.

To test out your temperature sensor, you would insert the sensor in the Analog 0 port, and run the scrip with something like

<pre class="lang:sh decode:true ">
sudo python ./grove_temperature_sensor.py
</pre>

&nbsp;

#  Your very own script using Grove

You'd might like your sensor data to be sent somewhere (and not just printed out in the terminal window).

What I did was to publish the sensor data with MQTT.

A typical script I have written lately might look like this:

<pre class="lang:python decode:true">
#!/usr/bin/env python

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

readTemperature()
</pre>

The basic concept is simple:

Every 5 seconds, read the temperature and publish it to the MQTT broker, on 192.168.10.200, with the topic "office/temperature".

If I have more than one sensor I just read and publish the data one at the time inside the try block.

&nbsp;

The important thing to notice here is that most of the work is done by the libraries I import. More specifically, the grovepi library, and the mqtt library (the publishing part of it).

&nbsp;

# Making the script run on startup

Once you have created a python script you want to run without interference (when you log out, restart or do whatever, you still want this script to run).

I have done this using something called upstart. I'll show you how to set that up properly.

&nbsp;

First, install upstart:

<pre class="lang:sh decode:true ">
sudo apt-get install upstart
</pre>

Then, you have to create an init configuration for your script.

<pre class="lang:sh decode:true ">
sudo nano /etc/init/sensors.conf
</pre>

<pre class="lang:default decode:true">
start on runlevel [2345]
stop on runlevel [016]

respawn
exec python /home/pi/code/sensors.py
</pre>

Just remember to change the path to your python script.

&nbsp;

This will make the sensors.py script run on startup, and if it ever crashes, it will restart by itself.

Reboot, and your script should run after startup.

To verify that your script is running:

<pre class="lang:sh decode:true ">
ps aux | grep sensors.py
</pre>

You should see something like this:

<pre class="lang:default decode:true ">
root 7157 0.7 2.0 11348 8936 ? Ss 03:59 3:38 python /home/pi/code/sensors.py
</pre>

You should also check with a MQTT client that your messages can be listened to.

&nbsp;

Now that you have a Raspberry Pi publishing sensor data, all you have to do is consume that data somehow. For instance with OpenHAB or some other home automation hub.

I hope this guide helped a bit with getting started with Raspberry Pi and Grove.