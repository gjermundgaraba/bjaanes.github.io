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

ES6, ES2015, or whatever you want to call it, introduced a new class syntax to the JavaScript world, 
and there has been quite a bit of controversy surrounding it. Some people even say you should never use it.
  
In this post, I will explain the new changes, where this controversy comes from,
and if there is anything to it.

<!--more-->

To really understand where all of this is coming from, you first have to understand JavaScript.
More importantly, you have to understand prototypal inheritance and a few patterns for creating objects in JavaScript.

# Prototypal vs classical inheritance

The first thing you need to understand is JavaScript's prototypal inheritance, and how it differs from classical inheritance.

If you have never heard about prototypal inheritance, I encourage you to read this article that explains it in very simple and easy-to-understand terms:
[A Plain English Guide to JavaScript Prototypes](http://sporto.github.io/blog/2013/02/22/a-plain-english-guide-to-javascript-prototypes/){:target="_blank"}
 
I will briefly go through the differences, though.

With *prototypal inheritance* you create sub classes from existing objects.
You use actual working objects to create new objects that inherits from it's parent.

With *classical inheritance*, you have a class, which is like a blueprint, from which other classes inherit. 
You create a hierarchy of classes you can use to create working instances.
It's important to keep in mind that a class is not actually an object, unlike the objects used with prototypal inheritance.

You can use the prototypal inheritance system to create something that looks like classical inheritance.
This is part of the reason some people don't like the new class syntax in JavaScript.

But we'll come back to that later.

# Some examples

I would like to show you some actual code, to demonstrate the syntactical diferrences between 
the old prototypal inheritance with function constructor, classical inheritance and of course the new ES6 (es2015) syntax. 

These three examples look and behave more or less the same way, and they all have more or less the same problems,
which again, I will come back to.

## Prototypal inheritance

The prototypal pattern with function constructors in JavaScript looks very similar to classical inheritance.

{% highlight javascript %}
function Phone(phoneNumber) {
  this.phoneNumber = phoneNumber;
}

Phone.prototype.call = function(receiver) {
  console.log("calling " + receiver + " from " + this.phoneNumber);
};
Phone.prototype.sendSms = function(receiver, message) {
  console.log("sending sms to " + receiver + " from " + this.phoneNumber);
};


function SmartPhone(phoneNumber) {
  Phone.call(this, phoneNumber);
}

SmartPhone.prototype = Object.create(Phone.prototype);
SmartPhone.prototype.surfWeb = function(url) {
  console.log("surfing the web on " + url);
};

var mySmartPhone = new SmartPhone(12345678);
mySmartPhone.call(987654321);
mySmartPhone.sendSms(987654321, "This is a text message!");
mySmartPhone.surfWeb("http://gjermundbjaanes.com");
{% endhighlight %}

To extend the Phone, you basically have to call the original constructor with the "call" method,
and set the SmartPhone prototype to be Phone's prototype, and then extend it manually.

While this is powerful, it *is* a bit hard to read. At least if you are not very familiar with this style.

It is also not the only way to do this. In fact, there are a bunch of different patterns you can use.
JavaScript experts urges you to use one or the other or a combination. It can be a bit confusing.
And I think it leads to many people not actually learning JavaScript in-depth.

For instance, you could create an object literal for the Phone, use Object.create and a factory function to achieve the exact same results:

{% highlight javascript %}
var phone = {
  call: function (receiver) {
    console.log("calling " + receiver + " from " + this.phoneNumber); 
  },
  sendSms: function (receiver, message) {
    console.log("sending sms to " + receiver + " from " + this.phoneNumber);
  }
};

var createSmartPhone = function (phoneNumber) {
  var smartPhone = Object.create(phone);
  smartPhone.surfWeb = function (url) {
    console.log("surfing the web on " + url);
  };
  smartPhone.phoneNumber = phoneNumber;
  
  return smartPhone;
};

function Phone(phoneNumber) {
  this.phoneNumber = phoneNumber;
}


var mySmartPhone = createSmartPhone(12345678);
mySmartPhone.call(987654321);
mySmartPhone.sendSms(987654321, "This is a text message!");
mySmartPhone.surfWeb("http://gjermundbjaanes.com");
{% endhighlight %}

This is also... fine... I guess. It's a mix of different stuff. I personally don't like it too much.
I think there are better options, at least most of the time. 

But I do like the factory functions a lot better than
constructor functions. The constructor functions have a lot of "magic" tied to it.

## Classical inheritance

The same structure could be created with classes in for instance Java like this:

{% highlight java %}
public class Phone {
  private int phoneNumber;

  public Phone(int phoneNumber) {
    this.phoneNumber = phoneNumber;
  }

  public void call(int reciever) {
    System.out.println("calling " + reciever + " from " + this.phoneNumber);
  }

  public void sendSms(int reciever, String message) {
    System.out.println("sending sms to " + reciever + " from " + this.phoneNumber);
  }
}

public class SmartPhone extends Phone {
  
  public SmartPhone(int phoneNumber) {
   	super(phoneNumber); 
  }
  
  public void surfWeb(String url) {
    System.out.println("surfing the internet on " + url);
  }
}
{% endhighlight %}

Slightly simpler and certainly looks more familiar to most people I assume.

## ES6 class syntax

Let's do the exact same example, only using the new ES6 class syntax:

{% highlight javascript %}
class Phone {
  constructor(phoneNumber) {
    this.phoneNumber = phoneNumber;
  }
  call(receiver) {
    console.log("calling " + receiver + " from " + this.phoneNumber);
  }
  sendSms(receiver, message) {
    console.log("sending sms to " + receiver + " from " + this.phoneNumber);
  }
}

class SmartPhone extends Phone {
  constructor(phoneNumber) {
    super(phoneNumber);
  }
  surfWeb(url) {
    console.log("surfing the web on " + url);
  }
}

var mySmartPhone = new SmartPhone(12345678);
mySmartPhone.call(987654321);
mySmartPhone.sendSms(987654321, "This is a text message!");
mySmartPhone.surfWeb("http://gjermundbjaanes.com");
{% endhighlight %}

This looks familiar, right? It looks a lot like the Java example.
Syntactically, it is almost the same. 

But it is not the same.

The class syntax is just syntactical sugar for the constructor function with prototype object.




Thoughts about this post thus far:

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


Another Thought: Composition is kind of lost with the class syntax.
The same is very true for constructor functions.
https://medium.com/javascript-scene/the-open-minded-explorer-s-guide-to-object-composition-88fe68961bed#.ih5zoksaz


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
http://chimera.labs.oreilly.com/books/1234000000262/ch03.html#delegate-prototype
 
 
Links:

* https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9#.887ugb292
* http://sporto.github.io/blog/2013/02/22/a-plain-english-guide-to-javascript-prototypes/
* http://alistapart.com/article/prototypal-object-oriented-programming-using-javascript
* https://github.com/joshburgess/not-awesome-es6-classes
* https://medium.com/@dan_abramov/how-to-use-classes-and-sleep-at-night-9af8de78ccb4#.g6whpdnj4
* https://news.ycombinator.com/item?id=8999372
* https://www.reddit.com/r/javascript/comments/3x91ac/why_not_to_hire_people_who_like_es6_classes/