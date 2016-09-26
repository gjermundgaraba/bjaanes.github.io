---
id: 279
title: Extending angular directives
date: 2015-06-07T19:09:13+00:00
author: Gjermund Bjaanes
layout: post
permalink: /extending-angular-directives/
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
  - 3829208144
categories:
  - CodeProject
  - Uncategorized
tags:
  - Angular
  - Programming
  - Web
---
In this post I will explain some techniques for extending Angular Directives and how to design for extensibility.

<!--more-->
It might not always make sense to go crazy and extend directives everywhere. Try not to use this more often than necessary. It’s no point making huge generic components just to call thing reusable. More often than not, it’s not even worth it to make things that generic. It all depends on the use case of course. Try to keep things small and reusable instead.

That said, when we do want to create some directive that is reusable and extendable, there exists many ways to do that. It all depends on you code style and what you actually want to extend.

All code created for this blog post is available on Github:
  
<a href="https://github.com/bjaanes/Extending-Directives-Blog-Post-Code" target="_blank">https://github.com/bjaanes/Extending-Directives-Blog-Post-Code</a>

# Require Directive for extension and decoration of controller

Let’s say you have a base directive of some sorts and you want to create a directive that extends the functionality of that base directive. Depending on what you want, using ‘require’ to decorate the base controller might solve your problems.

There are two very similar ways to do this:

## Separate Directive

Base Directive:

<pre class="lang:js decode:true" title="require.js">(function () {
    'use strict';

    angular
        .module('app')
        .directive('require', requireDirective);

    function requireDirective() {
        return {
            scope: {},
            restrict: 'AE',
            templateUrl: 'require/require.html',
            controller: RequireController,
            controllerAs: 'vm'
        };
    }

    function RequireController() {
        var vm = this;

        vm.data = [1, 2, 3];
        vm.doSomething = function () {
            console.log('RequireController Does Something');
            console.log(vm.data.toString());
        };

        vm.doSomethingElse = function () {
            console.log('RequireController does something else (?)')
        }
    }

})();</pre>

Directive template HTML:

<pre class="lang:xhtml decode:true" title="require.html">&lt;h1&gt;Require Directive&lt;/h1&gt;
&lt;button ng-click="vm.doSomething()"&gt;Do Something&lt;/button&gt;
&lt;button ng-click="vm.doSomethingElse()"&gt;Do Something Else&lt;/button&gt;</pre>

&nbsp;

Extension directive:

<pre class="lang:js decode:true ">(function () {
    'use strict';

    angular
        .module('app')
        .directive('requireExtension', requireExtensionDirective);

    function requireExtensionDirective() {
        return {
            restrict: 'A',
            require: 'require',
            link: function (scope, element, attributes, RequireController) {
                var originalDoSomething = RequireController.doSomething;

                RequireController.doSomething = function() {
                    console.log('Extension Does Something');
                    var number = RequireController.data.length + 1;
                    RequireController.data.push(number);
                    originalDoSomething();
                };

                RequireController.doSomethingElse = function () {
                    console.log('ONLY extension does something');
                }
            }
        };
    }

})();</pre>

Actual Usage:

<pre class="lang:xhtml decode:true ">&lt;require require-extension&gt;&lt;/require&gt;</pre>

&nbsp;

How it looks:

[<img class=" wp-image-283" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.38.18.png" alt="Require Screenshot" width="429" height="144" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.38.18.png 668w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.38.18-300x101.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.38.18-600x201.png 600w" sizes="(max-width: 429px) 100vw, 429px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.38.18.png)

What happens when you click Do Something:

<img class=" wp-image-284" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.39.39.png" alt="Console Screenshot Do Something" width="578" height="61" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.39.39.png 1118w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.39.39-300x32.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.39.39-1024x108.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.39.39-945x100.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.39.39-600x63.png 600w" sizes="(max-width: 578px) 100vw, 578px" />

&nbsp;

What happens when you click Do Something Else:

[<img class="alignnone wp-image-285" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.41.55.png" alt="Screenshot require Do Something Else" width="460" height="25" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.41.55.png 956w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.41.55-300x16.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.41.55-945x51.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.41.55-600x33.png 600w" sizes="(max-width: 460px) 100vw, 460px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.41.55.png)

## 

## Stacked Directive

Angular allows several directives with the same name to co-exists. Well, actually they all exist at the same time, so when you use one of them you use all of them at the same time.

Base Directive:

<pre class="lang:js decode:true ">(function () {
    'use strict';

    angular
        .module('app')
        .directive('requireStack', requireStackDirective);

    function requireStackDirective() {
        return {
            scope: {},
            restrict: 'AE',
            templateUrl: 'requireStack/requireStack.html',
            controller: RequireStackController,
            controllerAs: 'vm'
        };
    }

    function RequireStackController() {
        var vm = this;

        vm.data = [1, 2, 3];
        vm.doSomething = function () {
            console.log('RequireStackController Does Something');
            console.log(vm.data.toString());
        };

        vm.doSomethingElse = function () {
            console.log('RequireStackController does something else (?)')
        }
    }

})();</pre>

Directive template HTML:

<pre class="lang:xhtml decode:true ">&lt;h1&gt;Require Stack Directive&lt;/h1&gt;
&lt;button ng-click="vm.doSomething()"&gt;Do Something&lt;/button&gt;
&lt;button ng-click="vm.doSomethingElse()"&gt;Do Something Else&lt;/button&gt;</pre>

Extension directive:

<pre class="lang:js decode:true ">(function () {
    'use strict';

    angular
        .module('app')
        .directive('requireStack', requireStackExtensionDirective);

    function requireStackExtensionDirective() {
        return {
            restrict: 'AE',
            require: 'requireStack',
            link: function (scope, element, attributes, RequireStackController) {
                var originalDoSomething = RequireStackController.doSomething;

                RequireStackController.doSomething = function() {
                    console.log('Extension Does Something');
                    var number = RequireStackController.data.length + 1;
                    RequireStackController.data.push(number);
                    originalDoSomething();
                };

                RequireStackController.doSomethingElse = function () {
                    console.log('ONLY extension does something');
                }
            }
        };
    }

})();</pre>

Actual Usage:

<pre class="lang:xhtml decode:true ">&lt;require-stack&gt;&lt;/require-stack&gt;</pre>

&nbsp;

How it looks:

[<img class="alignnone wp-image-289" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.02.png" alt="Screenshot require stack directive" width="463" height="137" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.02.png 690w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.02-300x89.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.02-600x177.png 600w" sizes="(max-width: 463px) 100vw, 463px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.02.png)

What happens when you click Do Something:

[<img class="alignnone wp-image-291" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.36.png" alt="Screenshot require stack do something" width="646" height="68" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.36.png 1140w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.36-300x32.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.36-1024x108.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.36-945x99.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.36-600x63.png 600w" sizes="(max-width: 646px) 100vw, 646px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.36.png)

What happens when you click Do Something Else:

[<img class="alignnone wp-image-292" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.43.png" alt="Screenshot require stack do something else" width="630" height="21" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.43.png 1140w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.43-300x10.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.43-1024x34.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.43-945x32.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.43-600x20.png 600w" sizes="(max-width: 630px) 100vw, 630px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.56.43.png)

&nbsp;

Works exactly the same.

&nbsp;

# Generic Base Widgets and using delegates for functionality

<a href="http://gjermundbjaanes.com/angular-controller-communication-using-delegates/" target="_blank">I recently wrote about using delegate for controller communication.</a>

This is one the use cases where it might make sense. You can wrap your generic base directive inside a more specific directive which implements all the functionality that you need.

Directive for base:

<pre class="lang:js decode:true ">(function () {
    'use strict';

    angular
        .module('app')
        .directive('delegateBase', delegateBaseDirective);

    function delegateBaseDirective() {
        return {
            scope: {
                delegate: '='
            },
            restrict: 'AE',
            templateUrl: 'delegate/delegateBase.html',
            controller: DelegateBaseController,
            controllerAs: 'vm'
        };
    }

    function DelegateBaseController($scope) {
        var vm = this;

        vm.data = [1, 2, 3];
        vm.doSomething = function () {
            if ($scope.delegate && ('doSomething' in $scope.delegate)) {
                $scope.delegate.doSomething(vm.data);
            }
        };

        vm.doSomethingElse = function () {
            if ($scope.delegate && ('doSomethingElse' in $scope.delegate)) {
                $scope.delegate.doSomething();
            } else {
                console.log('No extension here, perhaps do some generic stuff instead?')
            }
        }

    }

})();</pre>

Directive template HTML:

<pre class="lang:xhtml decode:true ">&lt;h1&gt;DelegateBase Directive&lt;/h1&gt;
&lt;button ng-click="vm.doSomething()"&gt;Do Something&lt;/button&gt;
&lt;button ng-click="vm.doSomethingElse()"&gt;Do Something Else&lt;/button&gt;</pre>

Extension Directive with Delegate

<pre class="lang:js decode:true ">(function () {
    'use strict';

    angular
        .module('app')
        .directive('delegateExtension', delegateExtensionDirective);

    function delegateExtensionDirective() {
        return {
            restrict: 'AE',
            templateUrl: 'delegate/extension/delegateExtension.html',
            controller: DelegateExtensionController,
            controllerAs: 'vm'
        };
    }

    function DelegateExtensionController() {
        var vm = this;

        vm.delegateObj = {
            doSomething: function(data) {
                console.log('DelegateExtensionController Does Something');
                console.log(data.toString());
            }
        }
    }

})();</pre>

Extension Template HTML

<pre class="lang:xhtml decode:true ">&lt;h1&gt;Delegate Extension Directive&lt;/h1&gt;
&lt;delegate-base delegate="vm.delegateObj"&gt;&lt;/delegate-base&gt;</pre>

Actual usage:

<pre class="lang:xhtml decode:true ">&lt;delegate-extension&gt;&lt;/delegate-extension&gt;</pre>

&nbsp;

How it looks:

[<img class="alignnone wp-image-293" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.58.57.png" alt="Screenshot Delegate Extension" width="461" height="190" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.58.57.png 820w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.58.57-300x124.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.58.57-600x247.png 600w" sizes="(max-width: 461px) 100vw, 461px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.58.57.png)

What happens when you click Do Something:

[<img class="alignnone wp-image-294" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.02.png" alt="Screenshot delegate do something" width="715" height="47" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.02.png 1218w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.02-300x20.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.02-1024x67.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.02-945x62.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.02-600x39.png 600w" sizes="(max-width: 715px) 100vw, 715px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.02.png)

What happens when you click Do Something Else:

[<img class="alignnone wp-image-295" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.10.png" alt="Screenshot delegate do something else" width="743" height="27" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.10.png 1210w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.10-300x11.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.10-1024x37.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.10-945x34.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.10-600x22.png 600w" sizes="(max-width: 743px) 100vw, 743px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-20.00.10.png)

The reason for this last part is because I didn't implement the second delegate function. This might be useful if you want fallback functionality.

&nbsp;

# Transclude for extension of HTML

If you need to extend the HTML there are not that many options available to you. You basically have to utilize some sort of wrapping or even more likely transclusion in Angular.

Transclude in Angular directives is basically putting the markup that appears inside a directive somewhere where it makes sense.

<pre class="lang:xhtml decode:true">&lt;my-directive&gt;
    Some &lt;em&gt;Markup&lt;/em&gt;
&lt;/my-directive&gt;</pre>

&nbsp;

That can be utilized in my different ways, but in this case I assume you want a generic widget of some sorts that can be extended by putting html in certain places.

Let’s take the example of a header directive. Perhaps you need to use a header widget over several apps. You can create a simple base directive that takes some of the application-specific markup as transclusion.

## Simple (Single) Transclude

Directive:

<pre class="lang:js decode:true ">(function () {
    'use strict';

    angular
        .module('app')
        .directive('simpleTranslcude', simpleTranslcudeDirective);

    function simpleTranslcudeDirective() {
        return {
            transclude: true,
            restrict: 'AE',
            templateUrl: 'simpleTransclude/simpleTransclude.html'
        }
    }
})();</pre>

Directive template HTML:

<pre class="lang:xhtml decode:true ">&lt;h1&gt;Simple Transclude Directive&lt;/h1&gt;
&lt;div style="width: 100%; height: 50px; border: 1px solid; line-height: 50px;"&gt;
    &lt;img style="max-width:100%;max-height:100%;" src="angularlogo.jpg"&gt;
    &lt;div ng-transclude style="float: right"&gt;&lt;/div&gt;
&lt;/div&gt;</pre>

Actual Usage:

<pre class="lang:xhtml decode:true ">&lt;simple-translcude&gt;
    &lt;div&gt;
        &lt;button&gt;A Button&lt;/button&gt;
        &lt;button&gt;Another Button&lt;/button&gt;
    &lt;/div&gt;
&lt;/simple-translcude&gt;</pre>

&nbsp;

How it looks:

[<img class="alignnone wp-image-288" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.49.12.png" alt="Screenshot header directive transclude" width="660" height="131" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.49.12.png 1290w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.49.12-300x60.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.49.12-1024x203.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.49.12-945x188.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.49.12-600x119.png 600w" sizes="(max-width: 660px) 100vw, 660px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.49.12.png)

Everything on the left side of the header is now decided with the transcluded content. Nifty, eh?

&nbsp;

## Multiple Transclude

If you need to input HTML several places in a widget there are two options available:

### Split up the directive

The sane option usually. If it needs a lot of application specific stuff many places it might be better to split the directive up somehow

### Using multiple transclude

You could probably write some fancy link function that takes all the transcluded content and split it up with string manipulation (or something less error-prone), but luckily there exists a third-party solution to the problem:

ng-multi-transclude (https://github.com/zachsnow/ng-multi-transclude)

You can read about exactly how you can use it on the github page, but for now the code itself explains pretty good how things work:

You need to depend on ng-multi-transclude:

<pre class="lang:js decode:true ">(function () {
    'use strict';

    angular
        .module('app', ['multi-transclude']);
})();</pre>

Directive:

<pre class="lang:js decode:true ">(function () {
    'use strict';

    angular
        .module('app')
        .directive('multipleTransclude', multipleTranscludeDirective);

    function multipleTranscludeDirective() {
        return {
            transclude: true,
            restrict: 'AE',
            templateUrl: 'multipleTransclude/multipleTransclude.html'
        }
    }
})();</pre>

Directive template HTML:

<pre class="lang:xhtml decode:true ">&lt;h1&gt;Multiple Transclude Directive&lt;/h1&gt;
&lt;div ng-multi-transclude-controller style="width: 100%; height: 50px; border: 1px solid; line-height: 50px;"&gt;
    &lt;span ng-multi-transclude="left"&gt;&lt;/span&gt;
    &lt;div ng-multi-transclude="right" style="float: right"&gt;&lt;/div&gt;
&lt;/div&gt;</pre>

Actual usage:

<pre class="lang:xhtml decode:true ">&lt;multiple-transclude&gt;
    &lt;img name="left" style="max-width:100%;max-height:100%;" src="angularlogo.jpg"&gt;
    &lt;div name="right"&gt;
        &lt;button&gt;A Button&lt;/button&gt;
        &lt;button&gt;Another Button&lt;/button&gt;
    &lt;/div&gt;
&lt;/multiple-transclude&gt;</pre>

How it looks:

[<img class="alignnone wp-image-290" src="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.59.png" alt="Screenshot Multiple Transclude Directive" width="695" height="152" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.59.png 1234w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.59-300x66.png 300w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.59-1024x224.png 1024w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.59-945x207.png 945w, http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.59-600x131.png 600w" sizes="(max-width: 695px) 100vw, 695px" />](http://gjermundbjaanes.com/wp-content/uploads/2015/06/Screen-Shot-2015-06-07-at-19.54.59.png)

&nbsp;

# Extra

For some extra tips and tricks for extending directives you can check out the links below that I found while doing research for this topic.

Decorate the directive itself (the directive object with all the information):
  
<a href="http://stackoverflow.com/questions/19409017/angular-decorating-directives" target="_blank">http://stackoverflow.com/questions/19409017/angular-decorating-directives</a>

Using JavaScript Prototype for inheritance:
  
<a href="http://blog.mgechev.com/2013/12/18/inheritance-services-controllers-in-angularjs/" target="_blank">http://blog.mgechev.com/2013/12/18/inheritance-services-controllers-in-angularjs/</a>

Sources:
  
<a href="http://stackoverflow.com/questions/17005122/extending-angular-directive" target="_blank">http://stackoverflow.com/questions/17005122/extending-angular-directive</a>
  
<a href="https://github.com/angular/angular.js/wiki/Understanding-Directives" target="_blank">https://github.com/angular/angular.js/wiki/Understanding-Directives</a>
  
<a href="https://github.com/zachsnow/ng-multi-transclude" target="_blank">https://github.com/zachsnow/ng-multi-transclude</a>
  
<a href="http://zachsnow.com/#!/blog/2013/angularjs-multi-transclusion/" target="_blank">http://zachsnow.com/#!/blog/2013/angularjs-multi-transclusion/</a>