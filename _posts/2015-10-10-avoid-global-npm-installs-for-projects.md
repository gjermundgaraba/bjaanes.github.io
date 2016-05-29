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

I have recently moved gulp, karma and protractor away from my required installs in my <a href="https://github.com/bjaanes/ExtremeResults-WebApp" target="_blank">Extreme Results</a> app (which I wrote about here: <a href="http://gjermundbjaanes.com/learning-web-dev-series-part-5-extreme-results/" target="_blank">Learning Web Dev Series – Part 5: Extreme Results</a>). These things are now provided when running &#8220;npm install”.

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

Npm has a couple of script names that can be used without writing &#8220;run&#8221; in front of them, like start and test. For other words, you have to do it like this:

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

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_47">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Favoid-global-npm-installs-for-projects%2F&linkname=Avoid%20global%20npm%20installs%20for%20projects" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Favoid-global-npm-installs-for-projects%2F&linkname=Avoid%20global%20npm%20installs%20for%20projects" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Favoid-global-npm-installs-for-projects%2F&linkname=Avoid%20global%20npm%20installs%20for%20projects" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>