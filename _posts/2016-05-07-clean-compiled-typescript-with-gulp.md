---
id: 697
title: Clean compiled typescript with gulp
date: 2016-05-07T15:47:25+00:00
author: Gjermund Bjaanes
layout: post
guid: http://gjermundbjaanes.com/?p=697
permalink: /clean-compiled-typescript-with-gulp/
dsq_thread_id:
  - 4807848504
categories:
  - Uncategorized
tags:
  - Javascript
  - Web
---
This blog post will show you how you can clean your compiled TypeScript using gulp, if you compile your files inside your source folder.

<!--more-->

That means that this is applicable to you if your compiled output is placed next to the TypeScript files (which is what I am doing with [ExtremeResults](https://github.com/bjaanes/ExtremeResults-WebApp)).

That means that we will be able to clean out these sorts of structures:

<pre class="nums:false nums-toggle:false lang:default highlight:0 decode:true">someFile.ts (Original TypeScript file)
someFile.js (Compiled output)
someFile.js.map (Mapping file - also generated)
someFolder/someOtherFile.ts (Original TypeScript file)
someFolder/someOtherFile.js (Compiled output)
someFolder/someOtherFile.js.map (Mapping file - also generated)</pre>

Since these files are placed inside the source folder, it can be cumbersome to get rid of them in an automatic fashion.

I have two solutions prepared for this, both using Gulp.

&nbsp;

# First solution: search and replace

The first solution is kind of a &#8220;brute-force&#8221; solution. It takes a list of typescript files and create a new list of files by replacing the .ts with a .js. Not very intelligent, but it does the job.

&nbsp;

This is a solution that requires two dependencies: del and glob.

They can be installed like this:

<pre class="lang:sh decode:true ">npm install --save-dev del glob</pre>

&nbsp;

&nbsp;

This task does not get rid of map files, so you would need another one dealing with just the map files.

<pre class="lang:js decode:true ">gulp.task('clean-ts-generated', function (cb) {
  return glob('./src/app/**/*.ts', function (err, files) {
    var generatedFiles = files.map(function (file) {
      return file.replace(/.ts$/, '.js*');
    });

    del(generatedFiles, cb);
  });
});</pre>

This works, but is very manual, and a little ugly.

&nbsp;

# Second solution: Plugin

_gulp-clean-compiled-typescript_ is a gulp plugin I wrote and made available on npm. I did that just to be able to do the same as in the first solution, only cleaner.

Also, since I wrote it kind of generic, it might be of use to others! Open Source ftw!

&nbsp;

It achieves the same thing as the script above, but also takes care of .js.map files. It is also a lot simpler to use.

You just send in typescript files in a normal gulp way, and it gets rid of the appropriate files.

&nbsp;

You can install this plugin like this:

<pre class="lang:sh decode:true ">npm install --save-dev gulp-clean-compiled-typescript</pre>

&nbsp;

The use it, you can just do the following in your gulp file:

<pre class="lang:js decode:true ">var cleanCompiledTypeScript = require('gulp-clean-compiled-typescript');

gulp.task('default', function () {
  return gulp.src('./app/**/*.ts')
    .pipe(cleanCompiledTypeScript());
});</pre>

&nbsp;

Easy and clean. Just the way I like it.

If you want to take a look at the source code, go to the Github page:

<https://github.com/bjaanes/gulp-clean-compiled-typescript>

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_72">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fclean-compiled-typescript-with-gulp%2F&linkname=Clean%20compiled%20typescript%20with%20gulp" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fclean-compiled-typescript-with-gulp%2F&linkname=Clean%20compiled%20typescript%20with%20gulp" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fclean-compiled-typescript-with-gulp%2F&linkname=Clean%20compiled%20typescript%20with%20gulp" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>