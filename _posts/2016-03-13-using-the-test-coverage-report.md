---
id: 619
title: Using the test coverage report
date: 2016-03-13T20:43:12+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=619
permalink: /using-the-test-coverage-report/
suevafree_template:
  - right-sidebar
dsq_thread_id:
  - 4659614659
categories:
  - CodeProject
tags:
  - Express
  - Javascript
  - Node.js
  - Programming
  - TDD
  - Testing
---
In this post, I want to talk a little about how to get test coverage reports, and what you might want use them for.

<!--more-->
If you are not already writing tests, you might want to consider doing that. I am not going into why tests are good in this post, but there are many sources on the internet for more about just that.

&nbsp;

# What is it?

A test coverage report is a report you can get as part of you &#8220;test run&#8221; that tells you which part of your code you are covering while running your tests. It&#8217;s a tool to help you see which parts of you code you are actually testing.

It tells you how much of your program is covered. Which lines you hit, which conditionals you are going into, which of them you aren&#8217;t.

It can be used with unit tests, integration tests and even full end-to-end tests. You just run the tests and get a report back on what you covered with them.

&nbsp;

&nbsp;

But, what do you actually use the coverage report for?

Sure, it might be a nice tool for management to see how &#8220;tested&#8221; your application is, but that has little value for you as a developer. Or for the application it self.

I think it would be nice to use that coverage report for some really really useful things. And you can!

&nbsp;

# Finding untested parts of your application

It sounds straightforward (and it really is, but like everything, you got to be conscious about it).

You think you cover the most important logic and the most of the bad corner cases of said logic. But are you? Are you really?

&nbsp;

Lets take an example from my [Extreme Results Server](http://gjermundbjaanes.com/learning-web-dev-series-part-7-parse-shutting-down/):

I will use the coverage reports from my integration tests, because those are the only ones I am generating right now (even though I have lots of unit tests as well).

This is how the overall coverage report looks my controllers:

&nbsp;

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/03/Coverage.png" rel="attachment wp-att-620"><img class="alignnone  wp-image-620" src="http://gjermundbjaanes.com/wp-content/uploads/2016/03/Coverage.png" alt="Coverage for controllers" width="511" height="169" srcset="http://gjermundbjaanes.com/wp-content/uploads/2016/03/Coverage.png 1023w, http://gjermundbjaanes.com/wp-content/uploads/2016/03/Coverage-768x254.png 768w" sizes="(max-width: 511px) 100vw, 511px" /></a>

&nbsp;

Looks pretty OK. High percentage of the code is being tested, but there are some branches not being taken. Let&#8217;s take a look at a few of those.

More specifically, let&#8217;s look at the relatedForReflectionsController.js. It has 3 out 6 branches not being taken. Sounds like there might be some corner cases hiding there.

&nbsp;

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/03/CoverageMissing.png" rel="attachment wp-att-621"><img class="alignnone  wp-image-621" src="http://gjermundbjaanes.com/wp-content/uploads/2016/03/CoverageMissing.png" alt="Coverage Missing Branches" width="510" height="456" srcset="http://gjermundbjaanes.com/wp-content/uploads/2016/03/CoverageMissing.png 1025w, http://gjermundbjaanes.com/wp-content/uploads/2016/03/CoverageMissing-768x686.png 768w" sizes="(max-width: 510px) 100vw, 510px" /></a>

&nbsp;

The red parts are lines I don&#8217;t hit. You can also see the conditionals that are not being tested properly.

I am not hitting the errors that might happen in the database (Line 28 and 32). Perhaps not too easy to hit with Integration Tests, so I&#8217;ll probably leave those to the unit tests.

There is however one path that I really should have tested.

On line 4, I don&#8217;t hit the else block (the red line on line 41).

I should really write a tests that verifies that i get back a 400 status if I send in a bad typeName.

&nbsp;

I might have missed this if I didn&#8217;t have my coverage report.

The takeaway is that you can use the coverage report to find the things your are not actually testing.

You might find quite a few test cases that you could write to better you tests.

&nbsp;

# Making a game out of it

I think the percentage part of the coverage is quite fun. It feels like a game. Something to strive for.

&nbsp;

I tend to try to make the percentage higher for every commit. Perhaps I write a few extra tests to hit some extra lines and conditionals in the code here and there.

&nbsp;

I actually did this to my Extreme Results Web App. I always upped the percentage. And now i have 100% test coverage on it!

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/03/100pCoverage.png" rel="attachment wp-att-622"><img class="alignnone size-full wp-image-622" src="http://gjermundbjaanes.com/wp-content/uploads/2016/03/100pCoverage.png" alt="XR Web App Coverage" width="469" height="133" /></a>

I actually hit every single line of code in my application with my unit tests. That is cool! First time for me.

&nbsp;

But beware. Just because you have lots of tests, doesn&#8217;t mean the tests are good. You also have to write good tests that will fail if your application start doing something wrong.

But that is a different topic for another day.

&nbsp;

For now: Try to use that coverage for something useful, AND fun!

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_65">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fusing-the-test-coverage-report%2F&linkname=Using%20the%20test%20coverage%20report" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fusing-the-test-coverage-report%2F&linkname=Using%20the%20test%20coverage%20report" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fusing-the-test-coverage-report%2F&linkname=Using%20the%20test%20coverage%20report" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>