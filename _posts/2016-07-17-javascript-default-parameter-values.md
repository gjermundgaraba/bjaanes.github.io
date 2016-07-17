---
title: 'JavaScript - Default Parameter Values'
date: 2016-07-17T14:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /javascript-default-parameter-values/
categories:
  - Uncategorized
tags:
  -
---

Before ES6 (ES2015), there were really no *good* way to do default function parameter values
in JavaScript.

In this post I will describe the new syntax that might save you quite a bit of time!

<!--more-->

&nbsp;

# How we had to do it before ES2015

Before ES2015, we had to do something like this to get default parameter values:

{% highlight javascript %}
function add(a, b) {
    if (typeof a === 'undefined') {
        a = 0;
    }

    if (typeof b === 'undefined') {
        b = 0;
    }

    return a + b;
}

console.log(add()); // 0
console.log(add(42)); // 42
console.log(add(2, 2)); // 4
{% endhighlight %}

It could be done with a slightly different syntax as well, but the this is the general idea.
 
You would have to manually check if the parameters are set or not, and then set them.

&nbsp;

# How we can do it with ES2015

We can now skip all that manual, error-prone labor, and just define our default parameters
in a simple and intuitive way

{% highlight javascript %}
function add(a = 0, b = 0) {
    return a + b;
}

console.log(add()); // 0
console.log(add(42)); // 42
console.log(add(2, 2)); // 4
{% endhighlight %}

It's really that easy! And exactly how you would expect it look like.

There are however a few extra tricks and gotchas that you might want to know about.

&nbsp;

# Default parameters are evaluated at call time

The default arguments get evaluated every single time the function is called.

That means that you create a new object every time.

It also means you have to keep that in mind if you use functions in your default parameters.

For instance, take a look at the following example:

{% highlight javascript %}
var defaultValueToUse = 0;
function getMyDefaultValue() {
    defaultValueToUse += 1;
    return defaultValueToUse;
}

function test(a = getMyDefaultValue()) {
    console.log(a);
}

test(); // 1
test(); // 2
{% endhighlight %}

You might not have expected this behaviour, but since the parameters gets evaluated every time,
this kind of makes sense. 

Either way, it's good to know!

&nbsp;

# Parameters are available to later default parameters

Parameters that have been evaluated can be used in consequent default parameters. 
That way you can use previous inputs in interesting ways to formulate your default values. 

I didn't figure out a really good way to show this, so I just created a variation from the example on MDN
with some auto pluralisation. 

{% highlight javascript %}
function createAnimalStory(singular, plural = singular + 's', story = plural + ' are animals') {
    console.log(singular + ': ' + story);
}

createAnimalStory('Dog'); // Dog: Dogs are animals
createAnimalStory('Mouse', 'Mice'); // Mouse: Mice are animals
createAnimalStory('Aye-Aye', 'Aye-aies?', 'I don\'t even...'); // Aye-Aye: I don't even...
{% endhighlight %}

The point is that you can use previous parameters to construct later default parameters.

Might come in handy!

&nbsp;

# Sending in undefined does the same as sending in nothing

Another thing to keep in mind, is that if you send in undefined (intentionally, or otherwise)
to your function, the default value will be used.

In other words (or code rather):
{% highlight javascript %}
function toBeDefined(a = 'To be, or not to be') {
    console.log(a);
}

var unintentionallyUndefined;

toBeDefined(); // To be, or not to be
toBeDefined(undefined); // To be, or not to be
toBeDefined(unintentionallyUndefined); // To be, or not to be
{% endhighlight %}

I think the code says it all. Sending in undefined does the same as sending in nothing. 
Default value will be used.

I'm not sure if this is expected behaviour or not, but it's certainly something to be aware of.

&nbsp;

# Can you use default parameters yet?

As always with the "newer" standards, you have to make sure you can actually use the
new fancy syntax.

The site can help you figure out whether or not you can use default parameters for your target browser (or platform):
[ES6 Compatibility table](https://kangax.github.io/compat-table/es6/){:target="_blank"}

&nbsp;

Finally, if you want to read more about Default Parameters in JavaScript, MDN is always at your service:
[MDN Default Parameters](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Default_parameters){:target="_blank"}