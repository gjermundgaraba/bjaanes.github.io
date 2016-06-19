---
title: 'JavaScript - var, let and const - and when to use them'
date: 2016-06-19T18:50:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /javascript-var-let-and-const-and-when-to-use-them/
categories:
  - Uncategorized
tags:
  -
---
ES6 (ES2015) introduced the new keywords _let_ and _const_, to be used side by side with _var_.

In this post, we'll take a closer look at all three, how the differ, and when to use them.

<!--more-->

&nbsp;

With ES6, you can use the _let_ and the _const_ keyword in basically the same places
as you would the _var_ keyword.

But, what are the differences? 

To understand that, we first need to understand _var_ properly.

# The _var_ keyword

With _var_, the variables you create are function scoped.

That means that they are available inside the function it was created, as well as any nested functions.

To demonstrate this quickly, take a look at this code:

{% highlight javascript %}
function test() {
  var myFunctionScopedVariable = 42;
  
  console.log(myFunctionScopedVariable); // 42
  
  function nestedTest() {
    console.log(myFunctionScopedVariable); // 42
  }

  nestedTest();
}

test();
console.log(myFunctionScopedVariable); // ReferenceError: myFunctionScopedVariable is not defined
{% endhighlight %}

You can access the variable inside the function, and all nested functions, but not outside it.

As long as the variable is declared inside the function, it's available in the entire function.

Lets take a look at an example where this is slightly problematic:

{% highlight javascript %}
function test() {
  
  for (var i = 0; i < 3; i++) {
      var myFunctionScopedVariable = 42;
  }

  console.log(myFunctionScopedVariable); // 42
  console.log(i); // 3
}
{% endhighlight %}

Both the variable "i", and the variable "myFunctionScopedVariable" is available after the loop.

This is not so cool. It's almost never what you want. Ugh. 
It just feels wrong...

But that is they way that _var_ works.

&nbsp;

There is actually another quirk with _var_, and that is hoisting.
It's not really specific to _var_, but it's behaviour is a bit weird.

What hoisting does, is that it moves all declarations to the top of it's scope.
Not the actual initialization though.

What that means in practice, is that this code block:

{% highlight javascript %}
console.log(typeof test); // "function"

function test() {
  
  for (var i = 0; i < 3; i++) {
      var myFunctionScopedVariable = 42;
  }
}
{% endhighlight %}

will be changed to something like this:

{% highlight javascript %}
function test() {
  var i;
  var myFunctionScopedVariable;

  for (i = 0; i < 3; i++) {
      myFunctionScopedVariable = 42;
  }
}

console.log(typeof test); // "function"
{% endhighlight %}

But... But why? Because JavaScript, and that's just how it is.

&nbsp;

# The _let_ keyword

Now that you mostly understand what goes on with _var_, we can start
looking at _let_, and how it actually works, compared to _var_.

&nbsp;

The main difference between _var_ and _let_ is that _let_ is block scoped,
instead of function scoped. 

This means that a lot of the crazyness we saw above, is not going to happen
with _let_. Phew!

More specifically, a variable created with the _let_ keyword is available
inside the block it was created, and any nested blocks as well.

Also, it *acts* like it is not hoisted, but I'll come back to that.

&nbsp;

The first example still works the same way with _let_:

{% highlight javascript %}
function test() {
  let myFunctionScopedVariable = 42;
  
  console.log(myFunctionScopedVariable); // 42
  
  function nestedTest() {
    console.log(myFunctionScopedVariable); // 42
  }

  nestedTest();
}

test();
console.log(myFunctionScopedVariable); // uh, oh! Error still!
{% endhighlight %}


The second example, however, will now start throwing some errors our way:

{% highlight javascript %}
function test() {
  
  for (let i = 0; i < 3; i++) {
      let myFunctionScopedVariable = 42;
  }

  console.log(myFunctionScopedVariable); // Error, undefined
  console.log(i); // Error, undefined
}

test();
{% endhighlight %}

Sanity restored. This is most certainly what I wanted, and definitely what I meant.

And it's not only for functions and loops; this is the behaviour for all blocks.
This code explains it better:

{% highlight javascript %}
if (true) {
    let a = 1;
}

console.log(a); // ReferenceError: a is not defined

{
    let b = 2;
}

console.log(b); // ReferenceError: b is not defined;
{% endhighlight %}

&nbsp;

But there is also another difference I briefly mentioned earlier,
and that is that _let_ "pretends" not to be hoisted.

It actually is hoisted, but if you try to use it before it's actual 
declaration, an error will be thrown.

The space between the start of the block, and the declaration is called the 
"Temporal Dead Zone". Don't try to use varible in that zone.

Allow me to demonstrate:

{% highlight javascript %}
a = 1; // This works
b = 2; // Error: b is not defined

var a;
let b;
{% endhighlight %}

I personally think this is perfectly reasonable. But you have to keep
it in mind, especially if you are refactoring code.

There is one more example I would like to point out, and that is a special case
with _let_, that you might want to know about.

{% highlight javascript %}
for (var i = 0; i < 3; i++) {
    console.log("Inside the loop: " + i);
    setTimeout(function () { 
        console.log("Inside the timeout: " + i) 
    });
}
{% endhighlight %}

This will result in the following output:

{% highlight bash %}
Inside the loop: 0
Inside the loop: 1
Inside the loop: 2
Inside the timeout: 3
Inside the timeout: 3
Inside the timeout: 3
{% endhighlight %}

Well... That is unfortunate. It kind of makes sense, but given the powerful
closure patterns used in JavaScript, this kind of breaks the expectations, in my opinion.

You wouldn't really think that _let_ would fix this, but it turns out that it does!

The ES6 spec says that _let_ in a for loop is scoped not only to the loop, but to each iteration.

Which means that this code:
{% highlight javascript %}
for (let i = 0; i < 3; i++) {
    console.log("Inside the loop: " + i);
    setTimeout(function () { 
        console.log("Inside the timeout: " + i) 
    });
}
{% endhighlight %}

will result in the following output:

{% highlight bash %}
Inside the loop: 0
Inside the loop: 1
Inside the loop: 2
Inside the timeout: 0
Inside the timeout: 1
Inside the timeout: 2
{% endhighlight %}

Again, sanity resorted.

&nbsp;

# The _const_ keyword

Now that we know a lot about _var_ and _let_, let's take a look at the _const_ keyword.

&nbsp;

The difference between _let_ and _const_ is not too big.

In fact, all the differences between _var_ and _let_ are also true for _var_ and **_const_**.

In other words, _let_ and _const_ is almost the same. 
They are both block scoped and work the same way.

The only thing that makes _const_ different is that is a constant:

**A variable created with _const_ cannot be changed after it is initialized.** 

And just like constants in most languages (as far as I know...), you have to initialize it when you declare it.

{% highlight javascript %}
const a; // SyntaxError: Missing initializer in const declaration
const b = 42;
b = 43; // TypeError: Assignment to constant variable.
{% endhighlight %}

This is good, but you have to keep one thing in mind:

Objects in a _const_ variable are *not* immutable. 

That means that you can still do this:
{% highlight javascript %}
const obj = {
    ultimateQuestionOf: "Life, the Universe, and Everything",
    answer: 42
};

obj.answer = 43; // This is OK, obj is not immutable
console.log(obj.answer); // 43 
{% endhighlight %}

Which is fine, and also makes the const something that can be used in almost all cases.

&nbsp;

We now know how _var_, _let_ and _const_ work. We also know how they differ from each other.

It's time to figure out when exactly we should use the different ones. 

&nbsp;

# When to use _var_

I would say: **almost never**.

And I really mean that. I see very few good reasons why you might want to use _var_.

It would have to be because you really want function scoped variables. For the most part,
that's absolutely not necessary, and is only confusing.

_let_ and _const_ gives you all the functionality you actually need from _var_, but with none of the
weird edge cases you really wouldn't expect (unless you are already a complete JavaScript expert).

&nbsp;

# When to use _let_ and _const_

I grouped these two together, because their usage is dependent on when you wouldn't use the other.

Any variable that you *need* to redefine later should use _let_, and any other variable should for the
most part be _const_. If you make a mistake, most modern tools will give you a heads up anyways.

[![IntelliJ giving a heads up]({{ site.baseurl}}/img/posts/const-tool-help.png)]({{ site.baseurl }}/img/posts/const-tool-help.png)

# Summary

You should stop using _var_ as soon as you can. 

There are few good reasons to ever use it, if you have access to _let_ and _const_.

&nbsp;

I also think you should use _const_ whenever you can (whenever you don't need to reassign a variable).

_const_ should be your default choice, only using _let_ when you really have to.

It makes your code clearer and more explicit about it's variables.

&nbsp;

If you have any questions, comments or constructive criticism (I'd love to get my views 
challenged with a good discussion), reach out to me on twitter or in the comments.

You can find me on twitter here: [gjermundbjaanes](https://twitter.com/gjermundbjaanes/){:target="_blank"} 