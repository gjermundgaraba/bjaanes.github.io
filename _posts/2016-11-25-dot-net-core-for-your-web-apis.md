---
title: '.NET Core for your Web API&#39;s?'
date: 2016-11-25T20:00:00+02:00
author: Gjermund Bjaanes
layout: post
permalink: /dot-net-core-for-your-web-apis/
categories:
  - Uncategorized
---
I got the opportunity to speak at a local .NET meetup group recently, and I figured that as the .NET n00b that I am, it would be a great learning experience on many levels.

The premise of the talk was to find out if .NET Core could be a good solution for creating Web API's for the modern web stack. More precisely, could ASP.NET Core be used just as easily as for instance Node to create RESTful API's?

<!--more-->

If you want to just download the code and give it try for yourself, it should be fairly easy to set everything up.

As always, the code is available on GitHub:
[https://github.com/bjaanes/dotnet-core-api-talk](https://github.com/bjaanes/dotnet-core-api-talk){:target="_blank"}

[![Picture from the talk]({{ site.baseurl}}/img/posts/aspnet_talk.jpg)]({{ site.baseurl }}/img/posts/aspnet_talk.jpg)

You can also find the slides from the talk on the GitHub project (warning, they are in Norwegian):

PPTX: [https://github.com/bjaanes/dotnet-core-api-talk/blob/master/dotnet-core-foredrag.pptx](https://github.com/bjaanes/dotnet-core-api-talk/blob/master/dotnet-core-foredrag.pptx){:target="_blank"}

PDF: [https://github.com/bjaanes/dotnet-core-api-talk/blob/master/dotnet-core-foredrag.pdf](https://github.com/bjaanes/dotnet-core-api-talk/blob/master/dotnet-core-foredrag.pdf){:target="_blank"}

&nbsp;

# Why should I talk about .NET?

Like I mentioned in the introduction, I am not experienced in .NET. In fact, my experience mostly in Java, Node and front-end stuff.

So why should I talk about it? What gives me the right!?

The very fact that I am a beginner in .NET does not mean that I can't talk about my experience as a web developer in using .NET Core in a web context for the first time.

The idea is that a beginners mind might be more open to ideas than that of an expert. I might just have less bias towards .NET. 

I hear people say great things, but I am not colored in the same way as someone who has worked with .NET for a decade (or even just a few years). 
I just don't care if it's the best things ever or not, I just care about the truth, for me, as a web developer.



> In the beginner's mind there are many possibilities, in the expert's mind there are few.
>
> -- <cite>Shunryu Suzuki (Author of "Zen Mind, Beginner's Mind")</cite>

&nbsp;

# What are these REST API's?

In case you are not familiar with REST API's, or would like a refresher, I thought I could just quickly explain what it is.

REST stands for Representational State Transfer, and it's basically an architectural principle for communication. 
It's lays down some rules and things to follow. For instance, the communication needs to be stateless (e.g. no context about the users session is held on the server). 
There is more too it, but for the sake of this post, you don't need to think too much about it.

RESTful API's is REST put on the web, with HTTP. The basic gist of it is that you design URI's, or resources, and perform different HTTP calls, with different HTTP verbs, on them.

For instance:

- GET **/books**
    - Retrieve a list of books
    - books is the URI (resource), GET is the verb.
- DELETE **/books/123456**
    - Deletes a specific book (with id 123456)
    - books/id is the URI (resource), DELETE is the verb
    - Example of full URL: http://www.gjermundbjaanesbooks.com/api/books/123456

I don't want to get too deep into this right now. Hopefully you "get" kind of how it's supposed to work, but if you are confused, I urge you to go and learn more about this. Many people uses RESTful API's today.

&nbsp;

# How I did my research

I wanted to know if .NET Core could be a viable solution for your web API's. I already know Node and a few other options for creating RESTful API's, 
so I figured that comparing what I already know to what I learn would be a good way to answer the question.

I wanted to use code as my basis of research. Real experience is king.
Therefore I designed a really simple API and implemented it in Node, ASP.NET Core and Java. 
I also created a web client in Aurelia, mostly to have a simple way of triggering the API's - and as a bonus I got to learn a bit more about Aurelia.

As a note, the Java version is not heavily weighted in this post, because I don't feel like it provides too much value to the conversation.
I mostly wanted to see the differences. It's a lot of the same as .NET, but a bit harder to get started, and more stuff you have to know. 
Therefore it kind of fell out of scope for the research.

I wanted to focus on small servers and API's, not enterprise level scenarios. 
To contribute to that idea, I wanted to highlight how easy it was to get started with a project. 
If you have to spend a lot of time just getting started, a lot of the momentum falls away prematurely. This is especially important in smaller projects.

&nbsp;

# Getting started: Node

I used Yeoman to generate my Node project. As the generator I used one called "api".

The generator is made to create RESTful NodeJS API's with ES6, Mongoose and Express.

You can install Yeoman with

{% highlight bash %}
$ npm install -g yeoman
{% endhighlight %}

And the generator can be install with

{% highlight bash %}
$ npm install -g generator-api
{% endhighlight %}

And to create your initial project, all you have to do is:

{% highlight bash %}
$ yo api
{% endhighlight %}

and follow the instructions.

The starting project that comes out of this generator was quite... Complex. At least for a starting point, in my opinion.

Inheritance and lots of structure can be good in larger applications, but for most smaller API's, it might be overkill.

It felt a bit confusing navigation around, and certainly didn't feel like an *easy* starting point.

In the index file, the endpoint is configured to a router:
{% highlight javascript %}
...
const routes = require('./routes');

app.use('/', routes);
...
{% endhighlight %}

In the router, end points under the root resource (the / URI) are configured to more routers:
{% highlight javascript %}
...

const user  = require('./model/user/user-router');
const pet  = require('./model/pet/pet-router');

router.use('/user', user);
router.use('/pet', pet);

...
{% endhighlight %}

In each of the routers, the verbs are connected to a controller and a function on it:
{% highlight javascript %}
const controller = require('./user-controller');
const Router = require('express').Router;
const router = new Router();

router.route('/')
  .get((...args) => controller.find(...args))
  .post((...args) => controller.create(...args));

router.route('/:id')
  .put((...args) => controller.update(...args))
  .get((...args) => controller.findById(...args))
  .delete((...args) => controller.remove(...args));

module.exports = router;
{% endhighlight %}

The controller talks to the database and returns data to the response.

{% highlight javascript %}
const Controller = require('../../lib/controller');
const userFacade  = require('./user-facade');

class UserController extends Controller {}

module.exports = new UserController(userFacade);
{% endhighlight %}

Oh wait a minute. Where are the controller functions? 

Right... Inheritance. The base class has the answers:
{% highlight javascript %}
class Controller {
  constructor(facade) {
    this.facade = facade;
  }

  find(req, res, next) {
    return this.facade.find(req.query)
    .then(collection => res.status(200).json(collection))
    .catch(err => next(err));
  }
  
  ...
}

module.exports = Controller;
{% endhighlight %}

I prefer not to use inheritance
unless it provides some clarity. In this case I only think it provides reuse. When using it for more real code, the logic will probably not be the same
for each controller and the inheritance should probably go out the window.

The same goes for the models, which are inheriting from a base Model class.
 
It makes for less readable and understandable code. It might make sense in larger project, but even then I am sceptical.

There are other generators for NodeJS RESTful APIs, but most of them are too complex for my taste. 
It works, but it's just a bit too much. Keep it simple, people!

&nbsp;

# Getting started: ASP.NET Core

Again, Yeoman was used to generate the project. For the generator, I used the offical "aspnet" generator.

You can install Yeoman with

{% highlight bash %}
$ npm install -g yeoman
{% endhighlight %}

And the generator can be install with

{% highlight bash %}
$ npm install -g generator-aspnet
{% endhighlight %}

And to create your initial project, all you have to do is:

{% highlight bash %}
$ yo aspnet
{% endhighlight %}

Select "Web API Application" and follow the instructions.

The project that comes out of this generator is much more to my taste. 
**Really, really simple**. 

One class is all you need to actually read to understand the core. And the code is very clear and easy-to-read.

There are quite a few other files as well, but I have ignored most of them. The same actually goes for the node project, which is littered with all kinds of config files.

For me, it was super easy to just get started with the coding immediately. 
No need to do tutorials and learn a bunch of stuff. I could get on with the experimentation right away. Awesome!

{% highlight csharp %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;

namespace WebAPIApplication.Controllers
{
    [Route("api/[controller]")]
    public class ValuesController : Controller
    {
        // GET api/values
        
        [HttpGet]
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5
        
        [HttpGet("{id}")]
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values
        
        [HttpPost]
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5
        
        [HttpPut("{id}")]
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5
        
        [HttpDelete("{id}")]
        public void Delete(int id)
        {
        }
    }
}
{% endhighlight %}

If you want to change how the API works, all you have to is to fiddle around in here.

Want to create a new endpoint? Just create a new controller class with the correct attributes and restart the server.
Done!

This is how I want my starter projects to be. This negates the need for most basic tutorials. Just get started.

&nbsp;

# What I created to explore this

To explore the idea posed, I decided to focus on creating a small application based on very few "requirements". It was almost purely experimentation driven development (if that's a thing?).

The only thing I "designed" was a super simple CRUD REST API

- GET **/books**
    - Get a list of all books
    - Output: JSON
- POST **/books**
    - Create a new book
    - Input: JSON
    - Output: JSON
- PUT **/books/id**
    - Update an existing book
    - Input: JSON
    - Output: JSON
- DELETE **/books/id**
    - Delete an existing book

I create a web client to call my API. The client is able to switch between the servers by clicking a button. Very neat to show that the API's work in the same way.

The client is written with the Aurelia Framework. The project is generated by the Aurelia CLI. I did this only because I wanted to learn more about Aurelia. I already know AngularJS quite well, and have experience with Angular 2 as well, but new technology is always fun. I try to never miss an opportunity to learn something new.

[![Aurelia Client Screenshort]({{ site.baseurl}}/img/posts/aurelia_client_screenshot.png)]({{ site.baseurl }}/img/posts/aurelia_client_screenshot.png)

The API was implemented in ASP.NET, NodeJS and Java. The Java version was not really part of the talk, or this post, but it wanted to keep it around as reference.

I based the implementation of the REST API on the Yeoman projects mentioned earlier.

All implementations talk with a MongoDB server for persistence.

&nbsp;

# How it was to implement (Node vs ASP.NET)

Since I have experience with Node already, as well as the other normal libraries (Express, Mongoose, etc), I actually expected it would be **way** quicker to implement the server in Node.

Not really the case. I didn't actually measure the time spent, but it felt pretty close to equal. I spent quite a bit of time getting back **into** Node, even though it's not that long ago I coded actively on a Node server. I stumbled around with all the boilerplate and it took me a while to get into the groove.

And even then, I struggled more on Node than on ASP.NET. Not sure why this was the case, but for the most part, it felt easier to code the server in ASP.NET than Node.

It could be that this was a rather unique experience, but it was very interesting nonetheless. And it sure is a good sign for ASP.NET Core!

&nbsp;

# How to add new endpoints: Node

Adding a new endpoint, or resource, to Node will depend slightly on your project and design, but the gist of it is that have to:

Add new endpoint and add it to router:
{% highlight javascript %}
const demoRouter = require('./demo-router');
app.use('/api/demo', demoRouter);
{% endhighlight %}

Connect router to controller:

{% highlight javascript %}
const controller = require('./demo-controller');
const Router = require('express').Router;
const router = new Router();

router.route('/')
  .get((...args) => controller.doDemo(...args))

module.exports = router;
{% endhighlight %}

Do logic
{% highlight javascript %}
class DemoController {
  doDemo(req, res, next) {
    res.status(200).send('Demo, Demo, Get, Get!');
  }
}

module.exports = new DemoController();
{% endhighlight %}


While not an awful lot of code, there is some boilerplate code to talk of here. It concerns me slightly, because boilerplate code is not my favorite thing... 
I didn't even feel good about demoing this particular thing in my talk, because I would have to get some many things right. So I didn't.

Like I said, this might not be a huge deal, but it is interesting to note.

Call to Demo API using Postman:
[![Call to Demo API using Postman]({{ site.baseurl}}/img/posts/demo_api_node_screenshot.png)]({{ site.baseurl }}/img/posts/demo_api_node_screenshot.png)

&nbsp;

# How to add new endpoints: ASP.NET Core

All you have to do to add a new endpoint in ASP.NET Core is to create a new controller with a few attributes (fairly similar to annotations in Java, as far as I can understand).

Here is how a new controller could look:

{% highlight csharp %}
using Microsoft.AspNetCore.Mvc;

namespace WebAPIApplication.Controllers
{
    [Route("api/[controller]")]
    public class DemoController : Controller
    {
        // GET api/values
        
        [HttpGet]
        public string Get()
        {
            return "Demo, Demo, Get, Get!";
        }
    }
}
{% endhighlight %}

Well, that was easy...

Call to Demo API using Postman:
[![Call to Demo API using Postman]({{ site.baseurl}}/img/posts/demo_api_aspnet_screenshot.png)]({{ site.baseurl }}/img/posts/demo_api_aspnet_screenshot.png)

&nbsp;

# Validation: Node

Validating input from users in your API's are important. There are several approaches to this in Node and Express, but using a library for it probably is the best approach. You could always check the body of the object manually and send back errors for them, but it requires slightly more cumbersome code.

I decided to use a library called express-validator. It can be installed with npm:

{% highlight bash %}
$ npm install --save express-validator
{% endhighlight %}

To use it in your application you first have to add it as a middleware:

{% highlight javascript %}
const validator  = require('express-validator');
app.use(validator());
{% endhighlight %}

Then you have to run the validation on the request body, get the errors as a list and handle them.

The basic logic is as follows:
{% highlight javascript %}
requestHandlerFunction(req, res, next) {
    req.checkBody("title", "Invalid Title").isLength({ min: 3, max: 60 });
    const errors = req.validationErrors();
    if (errors) {
        // Handle errors and probably return a 400 with some information from the errors.
    }
}
{% endhighlight %}

This wasn't too bad! It kind of clutters up the controller, but that can be abstracted away if you want to.

Either way, the code is quite easy to read and understand. A good day for Node in other words!

&nbsp;

# Validation: ASP.NET Core

Validation was actually one the things I found hardest with ASP.NET Core, before I managed to find out exactly how it worked. There might be some documentation, tutorial and tooling issues for some things. I struggled a bit at least before I found out exactly how it works.

You start by adding attributes to fields in your View/Model. The object that you take in as your request body.

There is a bunch available, but in my API, I only used "StringLength" and "RegularExpression".

Set up the view with validation attributes:
{% highlight csharp %}
using System.ComponentModel.DataAnnotations;


namespace WebAPIApplication.Controllers
{
    public class BookView
    {
        public string Id { get; set; }

        [StringLength(60, MinimumLength = 3)]
        public string Title { get; set; }

        [StringLength(60, MinimumLength = 3)]
        public string Author { get; set; }

        [RegularExpression(@"(ISBN[-]*(1[03])*[ ]*(: ){0,1})*(([0-9Xx][- ]*){13}|([0-9Xx][- ]*){10})")]
        public string Isbn { get; set; }
    }
}
{% endhighlight %}

Once you have your validation attributes set up, you need to verify that the model has validated. You probably want to do that quite early in your controller methods.

You can check if the validation went through by doing

{% highlight csharp %}
if (ModelState.IsValid)
{% endhighlight %}

If it's not valid, you can find all your errors by looping through them.

{% highlight csharp %}
List<ErrorView> listOfErrors = new List<ErrorView>();
foreach (var modelError in ModelState)
{
    string propertyName = modelError.Key;
    if (modelError.Value.Errors.Count > 0)
    {
        ErrorView errorView = new ErrorView();
        errorView.ErrorMessage = "Invalid " + propertyName;
        listOfErrors.Add(errorView);
    }
}
return new BadRequestObjectResult(listOfErrors); // Returns 400
{% endhighlight %}

The logic is a bit more convoluted and ugly I think, but it's not too different from the node version.
The biggest problem I had with it was the apparent lack of good documentation on it. Or I might have missed it...

&nbsp;

# .NET Core for your Web API's?

So, to answer the initial question, is .NET Core a good alternative for you Web API's?

**Yes**. I think it's an excellent option for your RESTful API's.

It's super easy to get started and playing around with.

For .NET (or even Java) developers it might be an even easier sell, because they can keep all the JavaScript on the client and write OOP on the server.

Still, for traditional web developers, it could be a powerful option for your smaller API's. It might even be a really solid option for more enterpricy use cases.

That said, I haven't explored everything. Or close to it. There are many use cases that I haven't tried at all - for instance user handling, security, complex API's.
Even so, I would assume this technology is going to grow and accommodate most users, if it doesn't already.

If there is one thing I would like you to do with this, it's to just try it yourself. 
Install Yoeman and the aspnet generator and play around a bit. You might just like it.

All the code is on GitHub:
[https://github.com/bjaanes/dotnet-core-api-talk](https://github.com/bjaanes/dotnet-core-api-talk){:target="_blank"}
