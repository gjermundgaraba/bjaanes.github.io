---
title: 'JavaScript - Why Template Literals are Awesome'
date: 2016-06-26T20:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /javascript-why-template-literals-are-awesome/
categories:
  - Uncategorized
tags:
  -
---
Ever wondered if there was a better way to concatenate string in JavaScript than
to use + everywhere? 

Or a better way to create multiline string than to use \n everywhere?

Well, there is!

<!--more-->

# What are Template Literals

Template literals is a "new" syntax to the JavaScript standard, which
came in ES6 (ES2015).

They can do the same thing as the normal JavaScript string literals, but
they have a couple of new possibilities, which makes them **Awesome**!

The syntactical difference is that instead of single or double quotes, you
use "back-tics": `

{% highlight javascript %}
const normalStringLiteral = "This is a string literal";
const anotherNormalStringLiteral = 'Same thing, but using single quotes';

const templateLiteral = `This works the exact same way`;
{% endhighlight %}

This alone doesn't really bring any benefits though, so let's take a look at what
really makes these template literals so great!

&nbsp;

# String concatenation

String concatenation sucks with normal string literals.

Ever done something like this?

{% highlight javascript %}
const message = "Hello " + username + " and welcome to this web app";
{% endhighlight %}

This was just one variable, and it is still a bit ugly and hard to read.

The new template literals are great for string concatenation with variables.
Let's just see the same example with template literals:

{% highlight javascript %}
const username = "bjaanes";
const message = `Hello ${username} and welcome to this web app`;
console.log(message); // Hello bjaanes and welcome to this web app
{% endhighlight %}

This is better! Even if you don't know the syntax, you know
what is going to happen here. And it scales a lot better too!

The ${username} is a  template placeholder, and will be replaced 
at run-time with the proper variable.

You can also do your JavaScript expressions inside of the template placeholders,
so you could do stuff like this:

{% highlight javascript %}
const randomNumber = 21;

function findCurrentUsername() {
    return "bjaanes";
}

const message = `The answer you looked for ${findCurrentUsername()}, is ${randomNumber * 2}`;

console.log(message); // The answer you looked for bjaanes, is 42
{% endhighlight %}

&nbsp;

# Multiline strings

Have you ever had to construct a big multiline string with JavaScript?

Did it look like this?

{% highlight javascript %}
const multilineUglyness = "This is a multiline \nstring which is \nvery ugly";
console.log(multilineUglyness); 
// This is a multiline
// string which is
// very ugly
{% endhighlight %}

Or perhaps you wanted to make it more readable by doing something like this?

{% highlight javascript %}
const multilineUglyness = "This is a multiline\n"
+ "string which is\n"
+ "very ugly";
console.log(multilineUglyness);
// This is a multiline
// string which is
// very ugly
{% endhighlight %}

Luckily, there is a better solution with template literals (or this part of the article
would be pretty useless, right?).

You can just do it in the most natural way imaginable:

{% highlight javascript %}
const multilineUglyness = `This is a multiline
string which is
much less ugly`;
console.log(multilineUglyness);
// This is a multiline
// string which is
// much less ugly
{% endhighlight %}

Now that is much easier to read. No more ugly escape character or string
concatenation to create your multiline string variables.

# More functionality

There is actually even more advanced functionality to template literals,
but I believe most people won't be needing them on a regular basis.

This functionality is the ability to create your own special tag functions to which
the template literal is sent and processed, instead of just being concatenated.

Just to show you very briefly how this might look, take a look at the following simple example:

{% highlight javascript %}
function myOwnTagFunction(strings, ...values) {
    console.log(strings[0]); // "Easy as"
    console.log(strings[1]); // ""

    console.log(values[0]); // 6

    return 42; // Ignoring everything and returning my own stuff!
}

const message = myOwnTagFunction`Easy as ${1+2+3}`;
console.log(message); // 42
{% endhighlight %}

You can return whatever you want from the tag function actually; functions, objects, strings.
They are very powerful, but probably not something you need for every day use. Good to know though!

If you want to read a little bit more about tagged template literals, take a look at the developer docs 
on MDN:
[Tagged Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_template_literals){:target="_blank"}

# Summary

In this post, I have shown why template literals are a great tool for us
JavaScript developers. They are powerful, practical and easy to use!

They allow us to easily both concatenate and create multiline strings.