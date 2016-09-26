---
id: 60
title: Debugging Java Applets in IntelliJ IDEA
date: 2015-01-14T19:08:35+00:00
author: Gjermund Bjaanes
layout: post
permalink: /debugging-java-applets-in-intellij-idea/
dsq_thread_id:
  - 3420314064
categories:
  - CodeProject
  - Uncategorized
tags:
  - Java
  - Programming
---
Ever had the misfortune of having to debug Java Applets in combination with a web app? 

I recently did, and I thought I might as well share some tips on debugging them in IntelliJ IDEA.

<!--more-->
# Enable Remote Debugging in Java Plugin

Open Java Control Panel and go to "Java" tab and the click "View".

[![Java Control]({{ site.baseurl }}/wp-content/uploads/2015/01/javacontrol.png)]({{ site.baseurl }}/wp-content/uploads/2015/01/javacontrol.png) 

&nbsp;

In "Java Runtime Parameters” add the following line (one line):

<pre>-Djava.compiler=NONE -Xnoagent -Xdebug -Xrunjdwp:transport=dt_socket,address=2502,server=y,suspend=n</pre>

(Note, the address can be anything you want it to be, I used 2502)

[![Jave Environment Settings]({{ site.baseurl }}/wp-content/uploads/2015/01/javaenvsettings.png)]({{ site.baseurl }}/wp-content/uploads/2015/01/javaenvsettings.png) 

&nbsp;

# Add a remote Run Configuration in IntelliJ IDEA

In the menu select "Run" and select "Edit Configurations..."
  
Click the Plus sign and Select “Remote"

[![Add Remote Run Configuration]({{ site.baseurl }}/wp-content/uploads/2015/01/addremote.png)]({{ site.baseurl }}/wp-content/uploads/2015/01/addremote.png) 

&nbsp;

Change the "Port" number to 2502 (or whatever you picked in while enabling remote debugging in the Java Plugin) and select a name for your run configuration.

[![Remote Run Configuration]({{ site.baseurl}}/wp-content/uploads/2015/01/remote-settings.png)]({{ site.baseurl }}/wp-content/uploads/2015/01/remote-settings.png) 

&nbsp;

# Debug

Now you are ready to debug. Start up your Applet and then run your new configuration ("Run" and "Name Of Your Run Configuration"

&nbsp;

I found my help mostly from the following link:

[http://www.nakov.com/blog/2008/08/20/debugging-java-applets-in-eclipse/](http://www.nakov.com/blog/2008/08/20/debugging-java-applets-in-eclipse/){:target="_blank"} 