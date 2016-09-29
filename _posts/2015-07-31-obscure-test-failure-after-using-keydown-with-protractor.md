---
id: 341
title: Obscure test failure after using keyDown with protractor
date: 2015-07-31T15:01:14+00:00
author: Gjermund Bjaanes
layout: post
permalink: /obscure-test-failure-after-using-keydown-with-protractor/
dsq_thread_id:
  - 3992889454
categories:
  - Uncategorized
tags:
  - Angular
  - Javascript
  - Programming
---
Lately I have been writing a lot of protractor tests, both privately and on the job. I recently got the displeasure of hunting down an insanely obscure bug which literally showed itself several minutes after the problem actually occurred.

<!--more-->
I had several spec files, which ran just fine separat, but failed with very wierd errors.

Only after inserting probably a billion browser.sleep(500) everywhere did I notice that one of the tests deselected an element in a structure, instead of selecting it.

It was selected before the test was trying to select it, but instead of just nothing happening (which is what usually happens when you click an already selected element), it deselected it.

&nbsp;

Turns out that in some other test did this:

<pre class="lang:js decode:true">browser.actions().mouseMove(element).keyDown(protractor.Key.CONTROL).click().perform();</pre>

Innocent enough I though, but it turns out that keyDown is never released. So protractor ran with the CONTROL key pressed the entire time after that line.

Simple solution is to just use keyUp after you are done doing everything you need.

<pre class="lang:js decode:true">browser.actions().mouseMove(element).keyDown(protractor.Key.CONTROL).click().keyUp(protractor.Key.CONTROL).perform();</pre>