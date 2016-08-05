---
id: 611
title: How to mock and spy on a mongoose model (or any other object created by a constructor function)
date: 2016-03-06T17:30:04+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=611
permalink: /how-to-mock-and-spy-on-a-mongoose-model/
suevafree_template:
  - right-sidebar
dsq_thread_id:
  - 4639321623
categories:
  - CodeProject
tags:
  - Express
  - Javascript
  - Node.js
  - Programming
  - TDD
  - Testing
  - Web
---
Want to know how to mock and spy on objects created by a constructor? 

Allow me to show you!

<!--more-->

&nbsp;

I am currently writing a new back-end for my Extreme Results app using Node.js and Express. I wrote a little about why and how in my previous blog post: <a href="http://gjermundbjaanes.com/learning-web-dev-series-part-7-parse-shutting-down/" target="_blank">Learning Web Dev Series – Part 7: Parse shutting down</a>

I am of course writing unit tests all over the place, and to do that I am using Jasmine, which is the same framework I am using for the client (AngularJS app).

<img class="alignnone  wp-image-613" src="http://gjermundbjaanes.com/wp-content/uploads/2016/03/plural-of-mongoose.jpg" alt="Mongoose" width="388" height="259" />

&nbsp;

I have a MongoDB database, which is being communicated with using “<a href="http://mongoosejs.com/" target="_blank">mongoose</a>”.

Mongoose has models which are used for creating objects and querying them. In order to unit test the parts of the application using my mongoose models, I need to mock them out somehow.

I inject the models into my controllers, so what is the actual problem here?

&nbsp;

# Constructors and their baby objects

The problem is that these models are constructors used when creating a new object in the database. The code might look like this:

<pre class="lang:js decode:true">var outcomeController = function (OutcomeModel) {
    var post = function (req, res) {
        var outcome = new OutcomeModel(req.body); // Creating a new outcome here with the body of the request
        outcome.save(function (error) { ... }); // Saving the outcome here
    };
...</pre>

&nbsp;

I am injecting the model into a controller, which then makes it possible to inject a mock model when unit testing.

But the objects being created are not that easy to spy on with Jasmine.

How can i spy on the objects being created inside the controller?

&nbsp;

# Prototype to the rescue

Turns out that I can spy on the prototype, which makes this fairly easy.

I create my base mock like this in the top of my test file.

<pre class="lang:js decode:true ">OutcomeMock = function () {};
OutcomeMock.prototype.save = function () {};
OutcomeMock.prototype.remove = function () {};
OutcomeMock.prototype.validateSync = function () {};
OutcomeMock.find = function () {};</pre>

When I create my controllers in my tests, I just send in the OutcomeMock:

<pre class="lang:js decode:true ">var outcomeController = require('../../controllers/outcomeController')(OutcomeMock);</pre>

I can then spy on my outcome created inside the controller like this:

<pre class="lang:js decode:true">spyOn(OutcomeMock.prototype, 'save');</pre>

All the code is available on Github, so if you want to see how I do all my testing, take a look:

&nbsp;

[https://github.com/bjaanes/ExtremeResults-Server](https://github.com/bjaanes/ExtremeResults-Server){:target="_blank"}