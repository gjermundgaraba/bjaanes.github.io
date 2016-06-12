---
title: 'ES6 - Class vs Prototype'
date: 2016-06-12T15:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /es6-class-vs-prototype/
categories:
  - Uncategorized
tags:
  -
---

ES6, ES2016, or whatever you want to call it, introduced a new class syntax for the javascript world, 
and there has been quite a bit of controversy surrounding it. Some people even say you should never use it.
  
In this post, I will explain what these things are, and try to explore where this controversy comes from,
and if there is anything to it.

<!--more-->

Thoughts about this post thus far:

* Brief introduction to prototypal inheritance
    * Link to a more in-depth tutorial as well
* Brief introduction to ES6 class syntax
    * Explain that the ES6 class syntax is syntactical sugar for protoypal (come back to this point in conclusions) 
* Brief introduction to people saying ES6 classes are evil
* What I propose => es6 class is nice, but you need to know prototypal stuff

Don't use inheritance if you can avoid it anyways.
Favor composition over inheritance etc

Don't use classes or prototypes at all if it can be avoided.
In most cases, it might not be needed. If there are good use cases for it, let me know... 
If you want something to depend upon (because you miss static typing for instance), use TypeScript instead.

Classes seems to make sense for frameworks. Makes for kind of easy to look at code,
that is easy for Java programmers. But it might make them think it is normal classes.



Thought I want to explore:
Perhaps this quote is something people against classes are hiding behind.
Just becuase Douglas Crockford said it, doesn't mean it is true?
I am not sure how I feel about it just yet. I don't mind classes, but what are the 
real problems with the class syntax? Is it just because they sometimes
make people create classical inheritance? Or because people wont understand
prototypes? I want to explore this...

“If a feature is sometimes useful
and sometimes dangerous
and if there is a better option
then always use the better option.”
~ Douglas Crockford

https://medium.com/javascript-scene/10-interview-questions-every-javascript-developer-should-know-6fa6bdf5ad95#.pe533pal7
 
 
Links:
* https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9#.887ugb292
* http://sporto.github.io/blog/2013/02/22/a-plain-english-guide-to-javascript-prototypes/
* http://alistapart.com/article/prototypal-object-oriented-programming-using-javascript
* https://github.com/joshburgess/not-awesome-es6-classes
* https://medium.com/@dan_abramov/how-to-use-classes-and-sleep-at-night-9af8de78ccb4#.g6whpdnj4
* https://news.ycombinator.com/item?id=8999372
* https://www.reddit.com/r/javascript/comments/3x91ac/why_not_to_hire_people_who_like_es6_classes/