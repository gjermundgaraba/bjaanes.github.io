---
id: 629
title: Converting My Angular 1 Application to TypeScript
date: 2016-03-23T19:16:19+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=629
permalink: /converting-my-angular-1-application-to-typescript/
suevafree_template:
  - right-sidebar
dsq_thread_id:
  - 4687247592
categories:
  - CodeProject
  - Uncategorized
tags:
  - Angular
  - CI
  - CodeCoverage
  - Javascript
  - Programming
  - Testing
  - Web
---
With the soon-ish release of Angular 2, it makes sense to start upgrading Angular 1 apps to use TypeScript.

I have an Angular 1.x app called &#8220;Extreme Results&#8221;, which I want to upgrade to Angular 2 at some point. All the code mentioned in this post can be found in the GitHub repo for that app:

<a href="https://github.com/bjaanes/ExtremeResults-WebApp" target="_blank">https://github.com/bjaanes/ExtremeResults-WebApp</a>

&nbsp;

<a href="http://gjermundbjaanes.com/wp-content/uploads/2016/03/typescript-logo.png" rel="attachment wp-att-639"><img class="alignnone size-full wp-image-639" src="http://gjermundbjaanes.com/wp-content/uploads/2016/03/typescript-logo.png" alt="Typescript logo" width="250" height="61" /></a>

<a href="https://angular.io/docs/ts/latest/guide/upgrade.html" target="_blank">The Angular teams upgrade guide</a> says that one of the preparation steps for an update to Angular 2 is to migrate your app to TypeScript.

For this migration I have focused on the build steps, not actually writing anything in TypeScript specifically. This works out, because TypeScript is a super-set of JavaScript. All I really had to do for my source files was to rename them from fileName.js to fileName.ts.

The challenge in this migration was to get the build setup to compile the TypeScript files and still have everything work.

&nbsp;

So what actually needs to still work after migration?

  * **Development environement** 
      * I can still start a development server which automatically compiles and gets everything ready every time I save a file
      * No extra steps for development is crucial. It should not be more complicated to code, just because I use TypeScript!
  * **Distribution builds** 
      * Minification and everything compile with one simple command. It shall be no harder to create a proper build!
  * **Unit tests with coverage** 
      * This turned out the be the most difficult part to get right
      * Getting the tests to run properly was not that difficult, but coverage was not quite as easy as it required sourcemaps and an extra step before working.

&nbsp;

Now that we know what needs to work, lets get down to business!

&nbsp;

# Turn every file into TypeScript files

This was the easy part. Just rename every single file from fileName.**js** to fileName.**ts**.

I will later change them to actually use TypeScript functionality. Right now, TypeScript provides no value, but more on that in a later blog post.

If you see any errors while compiling later, you can safely just ignore them for now. We will fix that another time. Right now we will just focus on getting the build processes working with TypeScript.

&nbsp;

If I wanted to, I could have used typescript and compile everything manually, but I need it integrated into the build process I already have. Which brings me to the next step.

&nbsp;

# Bundles

I use something called gulp-bundle-assets to bundle all my files, which is used by the development environment and the distribution builds.

It basically bundles all javascript files together into smaller files (my own + 3rd party ones).

&nbsp;

For this to work, I needed to add an extra step in the build processs to compile all my TypeScript files into JavaScript.

I used a gulp plugin called gulp-typescript.

&nbsp;

I installed typescript and gulp-typescript with npm:

<pre class="lang:sh decode:true">npm install --save-dev typescript gulp-typescript</pre>

&nbsp;

I then added a the gulp task to do the actually compilation:

<pre class="lang:js decode:true ">gulp.task('typescript', ['clean'], function () {
    return gulp.src('src/app/**/*.ts')
        .pipe(typescript({
            target:'es5'
        }))
        .js
        .pipe(gulp.dest('tmp/typescript'));
    });</pre>

This compiles every .ts file into JavaScript (specifically ES5, which works on all browsers) and saves them to &#8216;tmp/typescript&#8217;.

&nbsp;

And then configured the gulp task to run before the bundle task.

<pre class="lang:js decode:true ">gulp.task('bundle', ['clean', 'templates', 'typescript'], function() {</pre>

&nbsp;

I also had to update my bundle configuration file to look for my compiled files instead of the normal JavaScript files (since they no longer exist).

<pre class="lang:js decode:true">scripts: [
    './tmp/typescript/app.js',
    './tmp/typescript/**/*.module.js',
    './tmp/typescript/**/*.js'
],</pre>

&nbsp;

This was actually everything that was required for development and distribution builds to work. The bundle task picks up all the compiled files and bundles them just like before.

If you don&#8217;t use bundles, you have to tweak this to make sense for you. Perhaps you have to point your development server to the compiled output folder, or something similar.

It should hopefully require little more effort than this, but you might have to find a solution that fits your particular build process.

&nbsp;

# Unit tests

The first step needed for unit tests to run was to point karma.conf.js to my compiled files, instead of the regular JavaScript files (which again, don&#8217;t really exist anymore).

This also means that you have to build before running tests.

If you are using Gulp or Grunt to start your tests, then you just have to make sure you perform the TypeScript compilation before you fire up Karma.

&nbsp;

So in karma.conf.js, all I had to do was:

<pre class="lang:js decode:true ">files: [
    ...,
    'tmp/typescript/**/*.module.js',
    'tmp/typescript/**/*.js',
]</pre>

&nbsp;

The tests now load the compiled files instead, and the tests run like they should. Huzzah!

&nbsp;

Everything works! Except for one thing&#8230;

&nbsp;

# Coverage

I used to get a proper coverage report right of the bat from Karma. I now had to change this a little bit, since the coverage needs to be on the TypeScript files, not the compiled JavaScript files.

To do this, I needed to do several things.

&nbsp;

## Create sourcemaps

When compiling TypeScript, you need to generate sourcemaps as well. This is farily easy and just requires a new gulp plugin that does everything for you.

I used gulp-sourcemaps and changed the typescript task to do the following:

<pre class="lang:js decode:true ">gulp.task('typescript', ['clean'], function () {
    return gulp.src('src/app/**/*.ts')
        .pipe(sourcemaps.init())
        .pipe(typescript({
            target:'es5'
        }))
        .js
        .pipe(sourcemaps.write({sourceRoot: __dirname + '/src/app'}))
        .pipe(gulp.dest('tmp/typescript'));
    });</pre>

&nbsp;

Notice that it does a _sourcemaps.init()_ before starting to compile the TypeScript files.

It then writes the sourcemaps to those files with a very particular sourceRoot.

The sourceRoot option in _sourcemaps.write_ makes sure that we find the sources from where the compiled output comes from.

This is needed because I output the compiled files to a different folder (tmp/typescript) than the source files (which can be found in src/app).

&nbsp;

## Create a coverage report for the tests

I will assume you have coverage reports already and have installed karma-coverage as well as configured it.

If not, take a look at my previous blog post about coverage: <a href="http://gjermundbjaanes.com/add-coverage-to-your-angular-project-to-show-on-your-github-page/" target="_blank">Add coverage to your Angular project</a>

&nbsp;

Before we can create a proper coverage report, we need to create one for the tests, which ran against the JavaScript files. This is done in Karma.

I still use karma-coverage to do this, but I now just use the output as a middle step to generate a proper report using the sourcemaps later.

&nbsp;

The karma configuration file now needs these changes:

<pre class="lang:js decode:true">preprocessors: {
     'tmp/typescript/**/*.js': ['coverage']
}</pre>

&nbsp;

<pre class="lang:js decode:true">coverageReporter: {
    type : 'json',
    subdir: '.',
    dir : 'coverage/'
}</pre>

&nbsp;

I now run the coverage against the compiled TypeScript files (in my tmp/typescript folder) and generate a JSON coverage report for those. This report is what I&#8217;ll be using in the next step.

&nbsp;

## Create a proper coverage report for the TypeScript files using sourcemaps

To create the proper report, I used a tool called remap-istanbul. I have not integrated this tool into any build processes other than creating an npm script for it.

The reason for this, is that I don&#8217;t really need the coverage report all the time.

I create them when I need them, and more specifically, I create them in Travis (my Continous Integration system) and send them to codecov to get a nice coverage badge in my <a href="https://github.com/bjaanes/ExtremeResults-WebApp/blob/master/README.md" target="_blank">GitHub README file</a>.

&nbsp;

The following npm script is all that is needed to generate a proper report:

<pre class="lang:js decode:true">"generateLcov": "remap-istanbul -b src/app/ -i coverage/coverage-final.json -o coverage/lcov.info -t lcovonly"</pre>

&nbsp;

&nbsp;

All I do is to create the coverage report is in my .travis.yml file:

<pre class="lang:default decode:true ">- npm run citest
- npm run generateLcov</pre>

&nbsp;

I could, and probably will create some HTML reports on the fly to get the most out of the coverage report:

<a href="http://gjermundbjaanes.com/using-the-test-coverage-report/" target="_blank">Using the test coverage report</a>

&nbsp;

&nbsp;

For more information on how to use remap-istanbul, take a look at:
  
<a href="https://github.com/SitePen/remap-istanbul" target="_blank">https://github.com/SitePen/remap-istanbul</a>

&nbsp;

# What now?

Well, now I have TypeScript, but with no benefits. No real value has been added to anything just ye. So that is the next step for the app. Actually using TypeScript to get some value.

I will come back with a follow-up blog post on just that.

But at least we CAN start writing TypeScript now, without having to worry about everything breaking apart.

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_66">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fconverting-my-angular-1-application-to-typescript%2F&linkname=Converting%20My%20Angular%201%20Application%20to%20TypeScript" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fconverting-my-angular-1-application-to-typescript%2F&linkname=Converting%20My%20Angular%201%20Application%20to%20TypeScript" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fconverting-my-angular-1-application-to-typescript%2F&linkname=Converting%20My%20Angular%201%20Application%20to%20TypeScript" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>