---
id: 252
title: Angular Controller Communication using Delegates
date: 2015-05-03T16:02:08+00:00
author: Gjermund Bjaanes
layout: post
permalink: /angular-controller-communication-using-delegates/
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
  - 3732759362
categories:
  - CodeProject
  - Uncategorized
tags:
  - Angular
  - Programming
  - Web
---
NOTE: This article is using $scope, but can easily be changed to use controllerAs syntax and bindToController instead. Please do. 

I recently found the need for two controllers to communicate a lot more than normal events would easily enable. I needed one controller to ask another for information, without them being too strongly coupled (because nobody likes that).

<!--more-->
There are several ways of solving this problem, but I found that using a delegate pattern was the most elegant solution for my problem.

&nbsp;

So the way this works is that a delegate object is sent to the controller that needs to be ‘asking the questions’, so that it knew where to get answers.

The delegate object comes from another controller that can help answer those questions.

&nbsp;

&nbsp;

<div id="attachment_254" style="width: 212px" class="wp-caption aligncenter">
  <a href="http://gjermundbjaanes.com/wp-content/uploads/2015/05/Untitled-Diagram-1.jpg"><img class="size-full wp-image-254" src="http://gjermundbjaanes.com/wp-content/uploads/2015/05/Untitled-Diagram-1.jpg" alt="Simple diagram showing how controller communication using delegates work" width="202" height="409" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/05/Untitled-Diagram-1.jpg 202w, http://gjermundbjaanes.com/wp-content/uploads/2015/05/Untitled-Diagram-1-148x300.jpg 148w" sizes="(max-width: 202px) 100vw, 202px" /></a>
  
  <p class="wp-caption-text">
    Simple diagram showing how controller communication using delegates work
  </p>
</div>

&nbsp;

The way this works is fundamentally very simple.

The Sub Controller needs someone to answer questions or do something that it cannot do by itself.

The reason it cannot do it, is probably because it shouldn’t be concerned with with how to get the answers. It’s job is to get a hold of the answer and display it (or use it for something at least).

Someone else knows how to answer the question. So it needs a delegate to do the job for it.

The Main Controller creates an object that is designed to work for the Sub Controller. How it gets the answer is not important. It can use a service to search for it elsewhere. It doesn’t matter. The point is that when the Sub Controller asks the question, the delegate is the one who will ultimately answer the question for the Sub Controller.

&nbsp;

For this to work, the Main Controller needs to send the delegate object to the Sub Controller. This is done using a directive isolate scope and bind a parent scope property to the isolate scope:

<pre class="lang:js decode:true ">.directive('myDirective', function () {
  return {
    scope: {
      delegate: '='
    },
    ...
  }</pre>

<pre class="lang:default decode:true ">&lt;my-directive delegate="someObjectThatCanWorkAsDelegate"&gt;&lt;/my-directive&gt;</pre>

The &#8216;=' allows the controller for myDirective to access the delegate on its isolate scope.

&nbsp;

The rest is just a matter of wiring things up and calling the correct stuff. I will show a simple example, that I have also implemented in a plunker: <a href="http://plnkr.co/edit/xNxScz8yy7SWQNk0r6RA?p=preview" target="_blank">http://plnkr.co/edit/xNxScz8yy7SWQNk0r6RA?p=preview</a>

Main Controller:

<pre class="lang:default decode:true">.controller('MainController', function ($scope) {
  var vm = this;
  vm.delegateObject = {
    getSeriousAnwser: function () {
      return "INSERT SERIOUS ANSWER HERE";
    },
    getJokeAnswer: function () {
      return "INSERT FUNNY JOKE HERE";
    }
  };
})</pre>

Directive with Sub Controller:

<pre class="lang:default decode:true">.directive('myDirective', function () {
  return {
    restrict: 'E',
    scope: {
      delegate: '='
    },
    controller: function ($scope) {
      var vm = this;
      vm.answer = 'no answer yet...';
      vm.getAnswer = function () {
        if (vm.joke) {
          vm.answer = $scope.delegate.getJokeAnswer();
        } else {
          vm.answer = $scope.delegate.getSeriousAnwser();
        }
              
      }
    },
    controllerAs: 'vm',
    template: 'Joke &lt;input type="checkbox" ng-model="vm.joke" &gt;' +
              '&lt;br&gt;&lt;button ng-click="vm.getAnswer()"&gt;Get Answer&lt;/button&gt;' +
              '&lt;br&gt;{{vm.answer}}'
  };
});</pre>

HTML:

<pre class="lang:default decode:true ">&lt;body ng-controller="MainController as vm"&gt;
  &lt;my-directive delegate="vm.delegateObject"&gt;&lt;/my-directive&gt;
&lt;/body&gt;</pre>

&nbsp;

I know there is not only one way to solve this sort of problem. You can in theory use events back and forth, but that will soon get very ugly and strongly coupled.

Another way, which seems to be popular, is to use a service like a messaging bus. I didn’t think it would be a good fit for the situation I was in, but it would certainly be better if you were not able to control the scopes and use directives in the same way as I do here.

It all depends on the situation.

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_27">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fangular-controller-communication-using-delegates%2F&linkname=Angular%20Controller%20Communication%20using%20Delegates" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fangular-controller-communication-using-delegates%2F&linkname=Angular%20Controller%20Communication%20using%20Delegates" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fangular-controller-communication-using-delegates%2F&linkname=Angular%20Controller%20Communication%20using%20Delegates" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>