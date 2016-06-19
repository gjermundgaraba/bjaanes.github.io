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
* Inheritance hierarchies are hard to reason about 
* Mention something about has-a is-a relationships
* The difference between is-a and has-a relationships is well known and a fundamental part of OOAD, but what is less well known is that almost every is-a relationship would be better off re-articulated as a has-a relationship.


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
        console.log("sending iMessage");
    }
}
{% endhighlight %} 

Looks "fairly" OK. This might even work. There are some issues with it, so let's go through them.

# 1 Hard to read and understand

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

I mean, re-use in general has this issue, but it's more isolated and can
be more easily tested for with composition. 

# 3 It creates inflexible designs

Software needs to be able to change, right?
Some way or another, software needs to be able to change.

Let's say a new iPhone comes to the market, and Apple has decided 
that iMessage is the only messaging platform that deserves to live.

Apple kills SMS on the iPhone.

Now what?

Our class structure assumed that every phone would have calling and SMS.
Suddenly the hierarchy is false.

Why did this happen? We tried to predict the future. And now we are locked
into this design we did "up-front".

There is no good way to normal classical inheritance to solve this problem.

# 4 It's harder to change behaviour at run-time

Inheritance creates a very static and rigid structure for your objects.

You can't change the behaviour of your objects at run-time.

Changing behaviour at run-time is especially important for testability.
Mocking out parts of your code is easy with dependency injection, but 
inheritance doesn't easily allow that.


# What is the alternative?

Compostion is the alternative to inheritance, and usually makes just as 
much sense, but mitigates many of the problems described above.

Let's take the same example, and add a the new iPhone without SMS, using composition.

In this example, I have abandoned the class keyword, in favor of factory functions.

You could still use classes, but I prefer this approach, since I get a bit more control.

{% highlight javascript %}
const callerFactory = function () {
    return {
        call: function () {
            console.log("making call");
        }
    }
};

const smsSenderFactory = function () {
    return {
        sendSms: function () {
            console.log("sending sms");
        }
    }
};

const webSurferFactory = function () {
    return {
        surfWeb: function () {
            console.log("surfing the web");
        }
    }
};

const iMessageSenderFactory = function () {
    return {
        sendIMessage: function () {
            console.log("sending iMessage");
        }
    }
};

const oldIPhoneFactory = function () {
    const iPhone = Object.assign(
        {},
        callerFactory(),
        smsSenderFactory(),
        webSurferFactory(),
        iMessageSenderFactory());
    return iPhone;
};

const iPhone8Factory = function () {
    const iPhone8 = Object.assign(
        {},
        callerFactory(),
        webSurferFactory(),
        iMessageSenderFactory());
    return iPhone8;
};

var iphone = oldIPhoneFactory();
iphone.sendSms();

var iPhone8 = iPhone8Factory();
iPhone8.sendIMessage();
iPhone8.sendSms(); // Won't work, iPhone8 does not have sendSms!
{% endhighlight %}

As you can see, the old iPhone and the new iPhone is created
using the Object.assign function from ES6.

All it does is combine a list of objects into the first argument (an empty object in this case).

# When to use inheritance

Now that you know why you might want to use composition over inheritance, and how to do it,
you might wonder if you should use inheritance at all.

The answer is as always. It depends...

I know, such a cop-out answer, but it's true.

Sometimes it is required by frameworks and languages.
Sometimes the code gets smaller and easier to understand with inheritance.

It all depends on the problem at hand. You just have to remember what you might be giving up.