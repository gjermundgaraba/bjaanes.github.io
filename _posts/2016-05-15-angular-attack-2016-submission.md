---
id: 709
title: Angular Attack 2016 Submission
date: 2016-05-15T21:41:45+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=709
permalink: /angular-attack-2016-submission/
dsq_thread_id:
  - 4829538770
categories:
  - Uncategorized
---
This post is about my submission to the Angular Attack 2016 Hackathon.

Here I am going to outline the solution that I have created and explain some technical details about how it all works.

<!--more-->

&nbsp;

More information about the hackathon can be found here:

[https://www.angularattack.com/](https://www.angularattack.com/){:target="_blank"} 

&nbsp;

During the hackathon, I created a web app that allows you view MQTT data in real time. I call it the MQTT Dashboard.

The app can be found at the following url:

[http://bjaanes.2016.angularattack.io/](http://bjaanes.2016.angularattack.io/){:target="_blank"} 

&nbsp;

A quick demo I created:

<iframe width="560" height="315" src="https://www.youtube.com/embed/wYjuudkOjxA" frameborder="0" allowfullscreen></iframe>

&nbsp;

# What is it?

The MQTT Dashboard allows the user to connect to any number of MQTT sources and topics and view the data beeing published in real time.

The app is written mainly with Angular 2 and TypeScript.

&nbsp;

[![MQTT Dashboard Screenshot]({{ site.baseurl}}/wp-content/uploads/2016/05/Screenshot.png)]({{ site.baseurl }}/wp-content/uploads/2016/05/Screenshot.png) 

&nbsp;

# What is MQTT?

MQTT is publish-subscribe light weight messaging protocol often used in IoT scenarios.

The protocol is based on one or more devices subscribing to “topics” and one or more devices publishing on “topics”. The subscribing devices get all messages for a specific topic that someone publishes on.

You also need a message broker to control the flow of all these messages.

In this case, the MQTT Dashboard can subscribe to many different brokers and topics at will.

A typical diagram of the MQTT architecture will look something like this:

[![MQTT Architecture Diagram]({{ site.baseurl}}/wp-content/uploads/2016/05/mqttdiagram.png)]({{ site.baseurl }}/wp-content/uploads/2016/05/mqttdiagram.png) 

For a little more information about MQTT and how I used it, take a look at a previous blog post I did about the subject:

[Smart Home Series Part 1 - Learning MQTT and buying stuff]({{ site.baseurl }}/smart-home-series-part-1-learning-mqtt-and-buying-stuff/){:target="_blank"} 

# How does it work?

The biggest technical challenge related to this app is the fact that most MQTT brokers do no support Websockets (some do, but that is not the most common today) and browsers do not support MQTT.

To solve this problem the app uses an MQTT Websocket bridge as it's backend.

&nbsp;

That means that the MQTT Dashboard connects to the backend with websockets, which deals with all the MQTT business that the browser cannot.

&nbsp;

Such a bridge already exists, but did not work exactly like needed for the app, so another version with a few modifications has been created here:

[https://github.com/bjaanes/mqtt-ws](https://github.com/bjaanes/mqtt-ws){:target="_blank"} 

&nbsp;

The architecture for the app then looks something like this:


[![MQTT Dashboard General Architecture]({{ site.baseurl}}/wp-content/uploads/2016/05/general-architecture.png)]({{ site.baseurl }}/wp-content/uploads/2016/05/general-architecture.png) 

&nbsp;

# What makes it special?

Two things in particular:

  * Allowing to connect to MQTT sources that doesn't support Websockets natively.
  * Allowing to connect to any number of sources and topics and viewing them real time with graphs

This makes this app an easy solution to monitor your MQTT topics in real time in a convenient manner.

&nbsp;

# Limitations

There are a few limitations that should be noted:

  * Only topics which output numbers will work (otherwise nothing of value will be shown)
  * Wildcard topics are not supported

&nbsp;

# Possible future improvements

The following improvements were considered but did not make it into the app during the hackathon:

  * Saving sources in local storage to persist between app instances
  * Support wildcard topics
  * Support different types of output from topics (text for instance)
  * Different types of graphs for each MQTT topic
  * Send MQTT messages to different topics and brokers in the app
  * Add more information to a source connection (like units for data)
  * More in-app help