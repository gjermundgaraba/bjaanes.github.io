---
id: 409
title: Avoid global npm installs for projects
date: 2015-10-10T16:27:52+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=409
permalink: /avoid-global-npm-installs-for-projects/
dsq_thread_id:
  - 4212734810
categories:
  - CodeProject
  - Uncategorized
tags:
  - Angular
  - Javascript
  - Programming
  - Web
---
Have you ever required gulp or grunt or something similar to be installed globally to be able to build a web project? You probably require npm as well? And possibly bower?

Having these kinds of global requirements is not healthy, nor is it very helpful. It’s much harder to get started with a project if there are many steps you have to follow, just to get all the requirements installed.

<!--more-->
Global installs might not be the right version all the time either. If you don't update, your local build might differ from the CI or even prod build.

There is a much better way that don’t require as much set up for a new dev environment.

&nbsp;

# npm

[<img class="alignnone wp-image-411" src="http://gjermundbjaanes.com/wp-content/uploads/2015/10/npm-logo.png" alt="npm logo" width="216" height="117" />](http://gjermundbjaanes.com/wp-content/uploads/2015/10/npm-logo.png)

What if you could just use npm for everything? The only thing you really need is node and npm (which usually comes with node.js anyways). The great answer here is npm scripts.

I have recently moved gulp, karma and protractor away from my required installs in my <a href="https://github.com/bjaanes/ExtremeResults-WebApp" target="_blank">Extreme Results</a> app (which I wrote about here: <a href="http://gjermundbjaanes.com/learning-web-dev-series-part-5-extreme-results/" target="_blank">Learning Web Dev Series – Part 5: Extreme Results</a>). These things are now provided when running "npm install”.

The way to still be able to run all your gulp tasks and whatnot, is by using npm scripts. For example, instead of doing

<pre class="lang:default decode:true">gulp serve</pre>

&nbsp;

to build, set up watchers and server, you could just do

<pre class="lang:default decode:true ">npm start</pre>

&nbsp;

&nbsp;

In package.json:

<pre class="lang:js decode:true ">"scripts": {
    "start": "gulp serve"
}</pre>

&nbsp;

Easy and nice!

&nbsp;

Npm has a couple of script names that can be used without writing "run" in front of them, like start and test. For other words, you have to do it like this:

<pre class="lang:default decode:true">npm run script_name</pre>

More information about npm scripts can be found here: <a href="https://docs.npmjs.com/misc/scripts" target="_blank">https://docs.npmjs.com/misc/scripts</a>

&nbsp;

These are the scripts I have right now:

<pre class="lang:js decode:true ">"scripts": {
    "clientdep": "bower install --no-interactive",
    "start": "gulp",
    "test": "gulp tdd",
    "selenium": "webdriver-manager update && webdriver-manager start",
    "e2e": "protractor protractor.conf.js"
},</pre>

&nbsp;

These can be run like this:

Installs all extra dependencies (from bower, since I am still using that, for now):

<pre class="lang:default decode:true ">npm run clientdep</pre>

&nbsp;

Build, watchers (automatically reload) and serve (local webserver for development):

<pre class="lang:default decode:true">npm start</pre>

&nbsp;

Run unit tests with watchers (automatically rereun tests):

<pre class="lang:default decode:true ">npm test</pre>

&nbsp;

Update web drivers and start a selenium server for protractor to use:

<pre class="lang:default decode:true ">npm run selenium</pre>

&nbsp;

Run e2e tests with protractor

<pre class="lang:default decode:true">npm run e2e
</pre>