---
title: 'BeaconMQTT - Bring context to your home automation system'
date: 2017-11-06T12:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /beaconmqtt/
categories:
  - Uncategorized
---

I recently released a brand new app on the Google Play store: BeaconMQTT.

The problem it solves is simple enough: Integrate Bluetooth Beacons into home automation systems.

<!--more-->

Check out the landing page: [BeaconMQTT Landing Page](http://beaconmqtt.gjermundbjaanes.com/){:target="_blank"}

The app is available today on [Google Play Store](https://play.google.com/store/apps/details?id=com.gjermundbjaanes.beaconmqtt){:target="_blank"}

&nbsp;

The idea is to use Bluetooth Beacons to bring context to your home automation system. Let the system know where you are (based on where your phone is).

For instance, you could turn on the light every time you enter a room. Or remind you to take out the trash if the trash is full when you leave the kitchen.

There are many use cases, but Bluetooth beacons have not been the easiest to get included in a home automation system - until now.

&nbsp;

# How it works

The app combines Bluetooth Beacons and the message protocol MQTT to bring context to any home automation system that can support MQTT.

The usage is fairly simple:
Clicking the + FAB you can search for and add any beacon the app supports (like an iBeacon or Estimote Beacon).

When the app detects that the beacon either enters or exits the area (or rather, your phone enters or exits the beacons range) it will be able to send an MQTT message to any MQTT broker you have configured.

[![BeaconMQTT Screenshot Main Screen]({{ site.baseurl}}/img/beaconmqtt/1.png)]({{ site.baseurl }}/img/beaconmqtt/1.png)

&nbsp;

# Features

1. Monitor in the background - no need to have the app open
2. Add custom names to beacons
3. Log events - for debugging of your system
4. Configure custom MQTT topics for enter and exit events
5. Show notifications on the phone (e.g. to test your beacon setup without having to think about MQTT)
6. Configure Beacon scanning to balance speed (time to detect) and battery life

[![BeaconMQTT Screenshot Log Screen]({{ site.baseurl}}/img/beaconmqtt/3.png)]({{ site.baseurl }}/img/beaconmqtt/3.png)

[![BeaconMQTT Screenshot Settings Screen]({{ site.baseurl}}/img/beaconmqtt/4.png)]({{ site.baseurl }}/img/beaconmqtt/4.png)

[![BeaconMQTT Screenshot Settings Screen]({{ site.baseurl}}/img/beaconmqtt/5.png)]({{ site.baseurl }}/img/beaconmqtt/5.png)

&nbsp;

# Try it now!

The app is available today on [Google Play Store](https://play.google.com/store/apps/details?id=com.gjermundbjaanes.beaconmqtt){:target="_blank"}