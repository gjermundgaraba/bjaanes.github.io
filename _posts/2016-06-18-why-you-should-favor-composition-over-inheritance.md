---
title: 'Why You Should Favor Composition Over Inheritance'
date: 2016-06-18T19:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /why-you-should-favor-composition-over-inheritance/
categories:
  - Uncategorized
tags:
  -
---
TODO: Write intro.

<!--more-->

Let's assume we are creating some sort of app that simulates phones of different types.

Phones have many common traits and functions, so we might be able to create some reusable base classes.

That is a reasonable first assumption, right? 
Maybe, but we are starting to predict the future and plan ahead already.

Still, we work from the assumption that we understand phones well enough that we can create a 
good class/object hierarchy. They don't change around that often. Right?

The code might looks something like this:

{% highlight javascript %}
class Phone {
  call(receiver) {
    console.log("making call");
  }
  sendSms(receiver, message) {
    console.log("sending sms");
  }
}

class SmartPhone extends Phone {
    surfWeb(url) {
        console.log("surfing the web");
    }
}

class IPhone extends SmartPhone {
    sendIMessage(receiver, message, fireworks) {
        console.log("testIMessage")
    }
}
{% endhighlight %} 

Looks "fairly" OK. This might even work. There are some issues with it, so let's go through them.

# 1 Hard to read

Even with this small and grossly simplified piece of code, 
it's kind of hard to track every moving piece. 

Just to figure out exactly what the "IPhone" can do, 
you have to move down the abstraction layers, one by one.

And if you want to use the functionality from base classes,
you have to know it is there, and how to use it. It forces 
you to have more stuff in your head at once, instead of on 
your screen.

Of course, modern IDE's help out. They have tons of tools to
get around these issues. But they aren't perfect, and
when you are reading, you want to try to do just that. 

# 2 Easy to break

Turns out, having all these fancy abstraction layers have some
downsides when it comes to making things more brittle. Without
very good unit tests, you can't really know for sure that a change
won't affect the rest of the hierarchy, going upwards.

I have to say, this is not completely fixed by using composition either,
but at least it is easier to track, than with deep inheritance structures. 

* Inheritance hierarchies are hard to reason about 

* Mention something about has-a is-a relationships