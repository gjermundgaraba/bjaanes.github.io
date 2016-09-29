---
id: 466
title: Add coverage to your Angular project (to show on your GitHub page)
date: 2015-11-22T15:30:37+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=466
permalink: /add-coverage-to-your-angular-project-to-show-on-your-github-page/
dsq_thread_id:
  - 4341199387
categories:
  - CodeProject
  - Uncategorized
tags:
  - Angular
  - CI
  - CodeCoverage
  - Javascript
  - Programming
  - TDD
  - UnitTests
---
Do you want to show off the amazing Code Coverage you got on you Angular project? Look no further, this guide will help you out!

<!--more-->
&nbsp;

# Prerequisites

You need a couple of things for this guide to make any sense to you:

  * Angular Project with tests running in Karma
  * Project on GitHub
  * Project building and testing in Travis

If you are missing any of these, don't worry, it can be easily fixed.

In particular, if you are not building and testing in Travis, you can refer to my guide where I showed you how to set it up:

<a href="http://gjermundbjaanes.com/how-i-set-up-continuous-integration-and-continuous-deployment-on-my-new-web-app-2/" target="_blank">How I set up Continuous Integration and Continuous Deployment on my new Web App</a>

&nbsp;

# Codecov

I recently set up code coverage with my project, [Extreme Results](http://gjermundbjaanes.com/learning-web-dev-series-part-5-extreme-results/).

I have been writing unit tests since day one, but had no way to show the coverage on the GitHub page.

And now, it looks like this (with a couple of other badges as well):

&nbsp;

[<img class="alignnone wp-image-467" src="http://gjermundbjaanes.com/wp-content/uploads/2015/11/XRGitHub.png" alt="Extreme Results GitHub page with badges" width="620" height="181" />](http://gjermundbjaanes.com/wp-content/uploads/2015/11/XRGitHub.png)

&nbsp;

Take a look for yourself too, it's pretty cool:

<a href="https://github.com/bjaanes/ExtremeResults-WebApp" target="_blank">https://github.com/bjaanes/ExtremeResults-WebApp</a>

&nbsp;

I had tried a couple of times previously to get this working, but I finally made it with a service called **Codecov**.

The rest of this guide will tell you how to set up your project to give that great code coverage report to Codecov, and show it on your GitHub page.

It's surprisingly easy when you just know what to do (just like anything, I guess, but still).

&nbsp;

# Setup

First thing you should do is register at codecov and link your project:
  
<a href="https://codecov.io/" target="_blank">https://codecov.io/</a>

Next, install the following dependencies from npm:

  * karma-coverage
  * codecov.io

&nbsp;

## Setting Up Karma

Next thing you have to do is to make sure Karma is producing a proper coverage result while running tests.

You need these parts in your karma.conf.js file:

<pre class="toolbar:2 lang:js decode:true">reporters: ['progress', 'coverage'],</pre>

<pre class="toolbar:2 lang:js decode:true">preprocessors: {
'src/app/**/*.js': ['coverage']
},</pre>

<pre class="toolbar:2 lang:js decode:true">coverageReporter: {
type : 'lcov',
dir : 'coverage/'
},</pre>

&nbsp;

and that you have the karma-coverage plugin in there:

<pre class="toolbar:2 lang:js decode:true">plugins: [
...
'karma-coverage',
...
]</pre>

&nbsp;

## Setting up Travis

Finally you have to set up Travis to run a couple of scripts.

You have to add the following lines to your .travis.yml file:

<pre class="toolbar:2 lang:default decode:true">before_install:
- pip install --user codecov
after_success:
- codecov</pre>

When you commit this code to GitHub, and Travis builds it, you should see the coverage report on Codecov update.

&nbsp;

## Updating Your README.md File

The last thing you probably want to to is to add the badge on your GitHub README file.

You just have to find a small snippet on Codecov.io under you project to add to your README file. This is quite simple:

&nbsp;

Open your project and click on the gears to the right on the page. Then select "Badge".

[<img class="alignnone wp-image-468" src="http://gjermundbjaanes.com/wp-content/uploads/2015/11/Codecov-Badge.png" alt="Codecov Badge Screenshot" width="530" height="445" />](http://gjermundbjaanes.com/wp-content/uploads/2015/11/Codecov-Badge.png)

You will then find some snippets you can use to show your badge. If you are updating a README.md file, you need the Markdown code.

Copy it and paste it into the top of your README.md file.

&nbsp;

[<img class="alignnone wp-image-469" src="http://gjermundbjaanes.com/wp-content/uploads/2015/11/Codecov-badge-2.png" alt="Codecov Badge Screenshot 2" width="530" height="171" />](http://gjermundbjaanes.com/wp-content/uploads/2015/11/Codecov-badge-2.png)

&nbsp;

**All done! Neat, right?**