---
id: 341
title: Obscure test failure after using keyDown with protractor
date: 2015-07-31T15:01:14+00:00
author: Gjermund Bjaanes
layout: post
guid: http://maximumdeveloper.com/?p=341
permalink: /obscure-test-failure-after-using-keydown-with-protractor/
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
  - 3992889454
suevafree_template:
  - right-sidebar
categories:
  - Uncategorized
tags:
  - Angular
  - Javascript
  - Programming
---
Lately I have been writing a lot of protractor tests, both privately and professionally. I recently got the displeasure of hunting down an insanely obscure bug which literally showed itself several minutes after it actually happened.

I had several spec files, which ran just fine separat, but failed with very wierd errors.

Only after inserting probably a billion browser.sleep(500) everywhere did I notice that one of the tests deselected an element in a structure, instead of selecting it.

It was selected before the test was trying to select it, but instead of just nothing happening (which is what usually happens when you click an already selected element), it deselected it.

&nbsp;

Turns out that in some other test did this:

<pre class="lang:js decode:true">browser.actions().mouseMove(element).keyDown(protractor.Key.CONTROL).click().perform();</pre>

Innocent enough I though, but it turns out that keyDown is never released. So protractor ran with the CONTROL key pressed the entire time after that line.

Simple solution is to just use keyUp after you are done doing everything you need.

<pre class="lang:js decode:true">browser.actions().mouseMove(element).keyDown(protractor.Key.CONTROL).click().keyUp(protractor.Key.CONTROL).perform();</pre>

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_39">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fobscure-test-failure-after-using-keydown-with-protractor%2F&linkname=Obscure%20test%20failure%20after%20using%20keyDown%20with%20protractor" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fobscure-test-failure-after-using-keydown-with-protractor%2F&linkname=Obscure%20test%20failure%20after%20using%20keyDown%20with%20protractor" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fobscure-test-failure-after-using-keydown-with-protractor%2F&linkname=Obscure%20test%20failure%20after%20using%20keyDown%20with%20protractor" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>