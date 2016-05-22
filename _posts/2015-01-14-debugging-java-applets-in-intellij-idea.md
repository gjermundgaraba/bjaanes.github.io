---
id: 60
title: Debugging Java Applets in IntelliJ IDEA
date: 2015-01-14T19:08:35+00:00
author: Gjermund Bjaanes
layout: post
guid: http://maximumdeveloper.com/?p=60
permalink: /debugging-java-applets-in-intellij-idea/
video_url:
  - 
audio_url:
  - 
quote_content:
  - 
quote_attribution:
  - 
link_url:
  - 
link_title:
  - 
dsq_thread_id:
  - 3420314064
suevafree_template:
  - right-sidebar
categories:
  - CodeProject
  - Uncategorized
tags:
  - Java
  - Programming
---
These are the steps I needed to take in order to debug Java Applets in IntelliJ IDEA.

# Enable Remote Debugging in Java Plugin

Open Java Control Panel and go to &#8220;Java&#8221; tab and the click &#8220;View&#8221;.

[<img class="alignnone wp-image-61" src="http://maximumdeveloper.com/wp-content/uploads/2015/01/javacontrol.png" alt="javacontrol" width="450" height="481" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/01/javacontrol.png 530w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/javacontrol-280x300.png 280w" sizes="(max-width: 450px) 100vw, 450px" />](http://maximumdeveloper.com/wp-content/uploads/2015/01/javacontrol.png)

&nbsp;

In &#8220;Java Runtime Parameters” add the following line (one line):

<pre>-Djava.compiler=NONE -Xnoagent -Xdebug -Xrunjdwp:transport=dt_socket,address=2502,server=y,suspend=n</pre>

(Note, the address can be anything you want it to be, I used 2502)

[<img class="alignnone size-full wp-image-64" src="http://maximumdeveloper.com/wp-content/uploads/2015/01/javaenvsettings.png" alt="javaenvsettings" width="553" height="329" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/01/javaenvsettings.png 553w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/javaenvsettings-300x178.png 300w" sizes="(max-width: 553px) 100vw, 553px" />](http://maximumdeveloper.com/wp-content/uploads/2015/01/javaenvsettings.png)

&nbsp;

# Add a remote Run Configuration in IntelliJ IDEA

In the menu select &#8220;Run&#8221; and select &#8220;Edit Configurations&#8230;&#8221;
  
Click the Plus sign and Select “Remote&#8221;

[<img class="alignnone wp-image-65" src="http://maximumdeveloper.com/wp-content/uploads/2015/01/addremote.png" alt="addremote" width="645" height="415" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/01/addremote.png 1092w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/addremote-300x193.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/addremote-1024x658.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/addremote-945x608.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/addremote-600x386.png 600w" sizes="(max-width: 645px) 100vw, 645px" />](http://maximumdeveloper.com/wp-content/uploads/2015/01/addremote.png)

&nbsp;

Change the &#8220;Port&#8221; number to 2502 (or whatever you picked in while enabling remote debugging in the Java Plugin) and select a name for your run configuration.

[<img class="alignnone wp-image-67" src="http://maximumdeveloper.com/wp-content/uploads/2015/01/remote-settings.png" alt="remote settings" width="643" height="413" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/01/remote-settings.png 1092w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/remote-settings-300x193.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/remote-settings-1024x658.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/remote-settings-945x608.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/01/remote-settings-600x386.png 600w" sizes="(max-width: 643px) 100vw, 643px" />](http://maximumdeveloper.com/wp-content/uploads/2015/01/remote-settings.png)

&nbsp;

# Debug

Now you are ready to debug. Start up your Applet and then run your new configuration (&#8220;Run&#8221; and &#8220;Name Of Your Run Configuration&#8221;

&nbsp;

I found my help mostly from the following link:

<http://www.nakov.com/blog/2008/08/20/debugging-java-applets-in-eclipse/>

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_5">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fdebugging-java-applets-in-intellij-idea%2F&linkname=Debugging%20Java%20Applets%20in%20IntelliJ%20IDEA" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fdebugging-java-applets-in-intellij-idea%2F&linkname=Debugging%20Java%20Applets%20in%20IntelliJ%20IDEA" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fdebugging-java-applets-in-intellij-idea%2F&linkname=Debugging%20Java%20Applets%20in%20IntelliJ%20IDEA" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>