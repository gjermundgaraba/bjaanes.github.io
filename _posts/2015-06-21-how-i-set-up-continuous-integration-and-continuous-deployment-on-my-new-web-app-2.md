---
id: 304
title: How I set up Continuous Integration and Continuous Deployment on my new Web App
date: 2015-06-21T11:01:36+00:00
author: Gjermund Bjaanes
layout: post
permalink: /how-i-set-up-continuous-integration-and-continuous-deployment-on-my-new-web-app-2/
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
  - 3866297397
categories:
  - Uncategorized
tags:
  - Programming
  - Web
---
I recently started working on a brand new web app. It has been a blast, but I wanted to be able to show the app off and test it, even when I am not in front of my development environment. Also, I really wanted all my tests to run every time I pushed to GitHub.

These things exists and are called Continuous Deployment (CD) and Continuous Integration (CI).

<!--more-->
Update: I Added how to set up the CI to run e2e tests with protractor.

# 

# Continuous Integration with Travis

For doing CI, I found a very popular service called Travis CI. It’s 10,000% free (according to their web site) for Open Source projects. It was super easy to set up. All I needed (almost) to do was to set up an account and connect to my Github Account.

The second thing I had to do for travis to work, was to set up a .travis.yml file. I have a pretty standard project so far, so I didn’t have to do much work to get set up there.

<pre class="lang:default decode:true">language: node_js
node_js:
  - "0.10"

before_script:
  - export DISPLAY=:99.0
  - sh -e /etc/init.d/xvfb start
  - webdriver-manager update
  - npm install
  - npm install -g bower
  - bower install
  - gulp &gt; /dev/null & # start server
  - sleep 10 # give server time to start


script:
  - node_modules/.bin/karma start karma.conf.js --no-auto-watch --single-run
  - node_modules/.bin/protractor protractor.conf.js --browser=firefox</pre>

&nbsp;

All it really does is set up what it needs to be able to run the tests with karma on Travis. It has a setup set called “before_script” where any installation and other preparation needs to happen. The “script” step is where you run your tests. I will soon add a new line for starting my protractor test suite.

It does some setup so that I can run Firefox (for tests), but the thing I had to add to make it work for me was the bower setup (“- npm install -g bower” and “- bower install”).

&nbsp;

## Protractor

I have set up Travis to run protractor as well. The most important parts of the script for this is the "gulp > /dev/null &" which builds the project and start a local web server (it might be done a different way for you).

In my case the default gulp task starts a web server locally at port 8080. I then have a param in my protractor.conf.js file like this:

<pre class="lang:js decode:true">exports.config = {
    params: {
        client: 'http://localhost:8080/'
    },
    ...
};</pre>

That way, the tests can do the following and still understand which web server to pick:

<pre class="lang:js decode:true ">browser.get(browser.params.client);</pre>

Finally, the tests are run using the:

<pre class="lang:default decode:true">- node_modules/.bin/protractor protractor.conf.js --browser=firefox</pre>

&nbsp;

<div id="attachment_308" style="width: 741px" class="wp-caption alignnone">
  <a href="http://maximumdeveloper.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.14.25.png"><img class=" wp-image-308" src="http://maximumdeveloper.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.14.25.png" alt="Screenshot from Travis website" width="731" height="205" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.14.25.png 1962w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.14.25-300x84.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.14.25-1024x287.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.14.25-945x265.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.14.25-600x168.png 600w" sizes="(max-width: 731px) 100vw, 731px" /></a>
  
  <p class="wp-caption-text">
    Screenshot from Travis website
  </p>
</div>

&nbsp;

Feel free to use my travis script, it was taken from the angular seed project:
  
<a href="https://github.com/angular/angular-seed" target="_blank">https://github.com/angular/angular-seed</a>

# 

# Continuous Deployment with dploy

I wanted my code to be pushed to a DigitalOcean droplet. The reason for that is because DigitalOcean is what I use to do these sort of things. It's also very cheap and easy to set up some droplets/vps for basically anything.

I started out by creating my account and connecting to GitHub and DigitalOcean.

After I had set up the dploy account I created a Droplet with the dploy and then created the deployment repository on my new dploy site.

On my droplet I installed node, npm, bower globally and gulp globally. I also installed a light weight web server called lighttpd. Not much setup needed. I just had to set up the environment on dploy to target /var/www on my droplet.

Finally, I had to set up a couple of Pre-launch commands to actually build the app.

<pre class="lang:default decode:true">npm install
bower install --allow-root --config.interactive=false
gulp build</pre>

Not much interesting. Installing npm dependencies, bower dependencies and then starting my gulp build script. Super easy!

&nbsp;

<div id="attachment_309" style="width: 735px" class="wp-caption alignnone">
  <a href="http://maximumdeveloper.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.13.41.png"><img class=" wp-image-309" src="http://maximumdeveloper.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.13.41.png" alt="Screen shot from dploy web site" width="725" height="976" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.13.41.png 1582w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.13.41-223x300.png 223w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.13.41-761x1024.png 761w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.13.41-945x1272.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-15-at-19.13.41-600x808.png 600w" sizes="(max-width: 725px) 100vw, 725px" /></a>
  
  <p class="wp-caption-text">
    Screenshot from dploy web site
  </p>
</div>

&nbsp;

The entire process took me no more than a couple of hours of fiddling, but it really feels good to have some automation set up. It will probably save me a lot of time later!

&nbsp;

&nbsp;

NOTE!

Dploy is now called DeployBot.

Since I wrote this article, the Digital Ocean API v.1 has been deprecated. The guide should still be valid.

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_33">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-i-set-up-continuous-integration-and-continuous-deployment-on-my-new-web-app-2%2F&linkname=How%20I%20set%20up%20Continuous%20Integration%20and%20Continuous%20Deployment%20on%20my%20new%20Web%20App" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-i-set-up-continuous-integration-and-continuous-deployment-on-my-new-web-app-2%2F&linkname=How%20I%20set%20up%20Continuous%20Integration%20and%20Continuous%20Deployment%20on%20my%20new%20Web%20App" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fhow-i-set-up-continuous-integration-and-continuous-deployment-on-my-new-web-app-2%2F&linkname=How%20I%20set%20up%20Continuous%20Integration%20and%20Continuous%20Deployment%20on%20my%20new%20Web%20App" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>