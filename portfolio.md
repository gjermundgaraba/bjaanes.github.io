---
title: Portfolio
author: Gjermund Bjaanes
layout: page
header-img: "img/portfolio_bg.png"
---

On this page, I wanted to just showcase a few of the projects I do **on my own time**.

All the code is available on GitHub: [https://gibhub.com/bjaanes](https://gibhub.com/bjaanes){:target="_blank"}.

# Extreme Results

This project was big enough that I have a separate sub page for it:
[http://gjermundbjaanes.com/xr](https://gjermundbjaanes.com/xr){:target="_blank"}

The project is also deployed on: [http://xr.gjermundbjaanes.com](https://xr.gjermundbjaanes.com){:target="_blank"}

Extreme Results is an Open Source software solution for implementing J.D Meier’s personal productivity system, Getting Results The Agile Way (Also called Agile Results).

[![Extreme Results Overview]({{ site.baseurl}}/img/portfolio/xr-portfolio.png)]({{ site.baseurl }}/img/portfolio/xr-portfolio.png)

It's a web app where I control the entire stack. Client and server written from scratch.

The app has a very rich automated test suite consisting of unit tests, integration tests and end-to-end tests.

I have a very high test coverage on all the code written.

- Technology
    - Server
        - Node.js
        - Express
        - MongoDB
        - Passport (for authentication)
        - Mocha
        - Jasmine
        - Gulp
    - Client
        - AngularJS
        - TypeScript
        - HTML
        - CSS
        - Jasmine
        - Protractor
        - SystemJS
        - jspm

Server Code: [https://github.com/bjaanes/ExtremeResults-Server](https://github.com/bjaanes/ExtremeResults-Server){:target="_blank"}

Client Code: [https://github.com/bjaanes/ExtremeResults-WebApp](https://github.com/bjaanes/ExtremeResults-WebApp){:target="_blank"}

&nbsp;

# BeaconMQTT

[![BeaconMQTT Logo]({{ site.baseurl}}/img/beaconmqtt/logo.png)]({{ site.baseurl }}/img/beaconmqtt/logo.png)

This is an Android app I created to solve the problem of integrating Bluetooth Beacons into home automation systems (using the IoT messaging protocol MQTT).

Using BeaconMQTT you can bring your Bluetooth Beacons into your home automation system. Whenever your phone is near or exits the area of a Beacon you can send an MQTT message. Perfect for bringing context into your home automation system!

[![BeaconMQTT Landing Page Screenshot]({{ site.baseurl}}/img/beaconmqtt/landingpage.png)]({{ site.baseurl }}/img/beaconmqtt/landingpage.png)

This is an app meant for developers and tinkerers using IoT and Home Automation.

[BeaconMQTT Landing Page](http://beaconmqtt.gjermundbjaanes.com/){:target="_blank"}

The app is available on [Google Play Store](https://play.google.com/store/apps/details?id=com.gjermundbjaanes.beaconmqtt){:target="_blank"}

&nbsp;

# Roommates

Roommates is an app for Android and iOS to make shared housing easier.

The apps were initially created as part of a group during my bachelor thesis. 
During that project, we didn't manage to finish all the features to make it ready for a proper release.

I took over the code base after the project and finished it on my own. The apps were available on their respective app stores for about 2 years.
I took down the apps because the Backend-as-a-service we used (Parse) shut down.

A landing page for the apps still exist here: [http://roommates.gjermundbjaanes.com/](http://roommates.gjermundbjaanes.com/){:target="_blank"}

[![Roommates]({{ site.baseurl}}/img/portfolio/roommates_portfolio.png)]({{ site.baseurl }}/img/portfolio/roommates_portfolio.png)

The code base consist of a native Android App, a native iOS app and Parse Cloud Code (written in JavaScript) for server side logic.

- Technology
    - Native iOS
        - Objective-C
        - Parse SDK
        - Facebook SDK
    - Native Android
        - Java
        - Parse SDK
        - Facebook SDK
    - Cloud Code
        - JavaScript
        - Parse SDK

Android Code: [https://github.com/bjaanes/Roommates-For-Android](https://github.com/bjaanes/Roommates-For-Android){:target="_blank"}

iOS Code: [https://github.com/bjaanes/Roommates-For-iOS](https://github.com/bjaanes/Roommates-For-iOS){:target="_blank"}

Parse Cloud Code: [https://github.com/bjaanes/Roommates-For-CloudCode](https://github.com/bjaanes/Roommates-For-CloudCode){:target="_blank"}

&nbsp;

# MQTT Dashboard

An MQTT Dashboard developed during the two-day hackathon Angular Attack 2016.

The app was a finalist among the about 300 entries, but did not win any prices. 
I was still most happy with the result. I learned a lot, and it was a lot of fun to participate.

A demo is available at [http://bjaanes.2016.angularattack.io/](http://bjaanes.2016.angularattack.io/){:target="_blank"}

I also wrote a blog post about the submission: [http://www.gjermundbjaanes.com/angular-attack-2016-submission/](http://www.gjermundbjaanes.com/angular-attack-2016-submission/){:target="_blank"}

The app allows you to monitor any MQTT topics in real time from anywhere (as long as they are available online)

The MQTT Dashboard allows the user to connect to any number of MQTT sources and topics and view the data the publish in real time.

The app is written mainly with Angular 2 and TypeScript.

The biggest technical challenge related to this app is the fact that most MQTT brokers do no support Websockets (some do, but that is not the most common today) and browsers do not support MQTT.

To solve this problem the app uses an MQTT WebSocket bridge as it's backend. That means that the MQTT Dashboard connects to the backend with websockets, which deals with all the MQTT business that the browser cannot.

Such a bridge already exists, but did not work exactly like needed for the app, so I forked the original and updated it to work the way I needed it to.

What makes this project special is 2 things in particular:
                        
1. Allowing to connect to MQTT sources that doesn't support Websockets natively.
2. Allowing to connect to any number of sources and topics and viewing them real time with graphs

[![MQTT Dashboard Screenshot]({{ site.baseurl}}/img/portfolio/mqtt_dashboard_portfolio.png)]({{ site.baseurl }}/img/portfolio/mqtt_dashboard_portfolio.png)

- Technology
    - Client
        - Angular 2
        - TypeScript
        - SystemJS
        - Highcharts
        - WebSockets
        - MQTT
    - MQTT Bridge
        - Node.js
        - WebSockets
        - MQTT

Client Code: [https://github.com/bjaanes/angularattack2016-bjaanes](https://github.com/bjaanes/angularattack2016-bjaanes){:target="_blank"}

MQTT Bridge Code: [https://github.com/bjaanes/mqtt-ws](https://github.com/bjaanes/mqtt-ws){:target="_blank"}

&nbsp;

# gulp-clean-compiled-typescript

Gulp plugin that cleans compiled output from typescript files (.js + js.map files).

This is a small plugin I wrote to help myself in the Extreme Results project. It is available on npm and is used by quite a few people:
[https://www.npmjs.com/package/gulp-clean-compiled-typescript](https://www.npmjs.com/package/gulp-clean-compiled-typescript){:target="_blank"}

- Technology
    - JavaScript
    - Gulp

Gulp Plugin Code: [https://github.com/bjaanes/gulp-clean-compiled-typescript](https://github.com/bjaanes/gulp-clean-compiled-typescript){:target="_blank"}

&nbsp;

# Goodreads Backup

This project started as a simple python script to be able to download all my book shelves from Goodreads.

It ended up as a two-part project with a script and a simple web app to operate it.

The Goodreads Backup app let's you enter your Goodreads User ID and get back a zip file containing a CSV file for each of your shelves. 

A demo can be found here: [http://demo.gjermundbjaanes.com:8080/goodreads-backup/](http://demo.gjermundbjaanes.com:8080/goodreads-backup/){:target="_blank"}

[![Goodreads Backup Screenshot]({{ site.baseurl}}/img/portfolio/goodreads-backup-portfolio.png)]({{ site.baseurl }}/img/portfolio/goodreads-backup-portfolio.png)

The python script downloads and processes your Goodreads shelves using the Goodreads API. It then saves each of them as a CSV file.

The reasoning for writing this script was that Goodreads seems to have some pretty buggy apps, and I don't completly trust them with keeping all my data safe. 
My to-read list is especially important for me to not lose.

The web app I created mostly to let others use the functionality I created a bit easier.

The script fetches all your books from all shelves and saves them to separated CSV files.

- Technology
    - Script
        - Python
        - XML (DOM Parsing from Goodreads API's)
    - Web app
        - Java
        - Spring Boot
        - HTML/CSS/JavaScript + jQuery
    

Goodreads Backup Script: [https://github.com/bjaanes/goodreads-backup](https://github.com/bjaanes/goodreads-backup){:target="_blank"}

Goodreads Backup Web: [https://github.com/bjaanes/goodreads-backup-web](https://github.com/bjaanes/goodreads-backup-web){:target="_blank"}

&nbsp;

# Raffle App

Simple Web App made with Meteor.js to allow for small raffles.

The app is a fun little application if you need to run any kind of raffles.
When the raffle price is drawn a drum roll is played to make it exciting.

It's quite configurable for any kinds of items and limitations to raffles (maximum number of items for instance).

The app also has an extensive statistics page to show fun metrics over time.

[![Raffle Overview]({{ site.baseurl}}/img/portfolio/raffle_list_portfolio.png)]({{ site.baseurl }}/img/portfolio/raffle_list_portfolio.png)

[![Raffle Drawing]({{ site.baseurl}}/img/portfolio/raffle_draw_portfolio.png)]({{ site.baseurl }}/img/portfolio/raffle_draw_portfolio.png)

- Technology
    - Meteor.js
    - JavaScript
    - HTML
    - CSS
    - MongoDB

Raffle App Code: [https://github.com/bjaanes/Raffle](https://github.com/bjaanes/Raffle){:target="_blank"}

&nbsp;

# .NET Core for your Web API's?

I did a session on a local .NET meetup group where I shared my experience with using ASP.NET Core for RESTful API's.

[![Raffle Drawing]({{ site.baseurl}}/img/portfolio/aspnet_talk.jpg)]({{ site.baseurl }}/img/portfolio/aspnet_talk.jpg)

The premise of the talk was to find out if .NET Core could be a good solution for creating Web API’s for the modern web stack. 
More precisely, could ASP.NET Core be used just as easily as for instance Node to create RESTful API’s?

Another aspect of the talk was that I had no experience with .NET from before. This made the learning experience quite interesting, I think.

I created a web client, and implemented a simple RESTful API in Node.js, .NET Core (ASP.NET Core) and Java. I then explored the viability of each option.

I wrote a blog post about the subject: [http://www.gjermundbjaanes.com/dot-net-core-for-your-web-apis/](http://www.gjermundbjaanes.com/dot-net-core-for-your-web-apis/){:target="_blank"}

The talk was in Norwegian, and the slide are too.

All the code, and the slides, are available on GitHub:

[https://github.com/bjaanes/dotnet-core-api-talk](https://github.com/bjaanes/dotnet-core-api-talk){:target="_blank"}