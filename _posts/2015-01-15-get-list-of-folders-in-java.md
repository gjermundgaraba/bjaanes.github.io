---
id: 75
title: Get list of folders in Java
date: 2015-01-15T18:27:47+00:00
author: Gjermund Bjaanes
layout: post
permalink: /get-list-of-folders-in-java/
video_url:
  - 
audio_url:
  - 
quote_content:
  - 
quote_attribution:
  - 
link_url:
  - 
link_title:
  - 
dsq_thread_id:
  - 3428808236
categories:
  - CodeProject
  - Uncategorized
tags:
  - Java
  - Programming
---
If you need to list only the folders in some directory (and not folders AND files), that can be done without too much effort in Java.

<!--more-->
The key is use File's listFiles with a FileFilter:

<pre class="nums:false lang:default decode:true">public File[] listFiles(FileFilter filter)</pre>

You can create an anonymous class like this to pass to your File object.

<pre class="lang:java decode:true">FileFilter directoryFileFilter = new FileFilter() {
    public boolean accept(File file) {
        return file.isDirectory();
    }
};</pre>

When you now call listFiles with the "directoryFileFilter", you will get a list of the folders inside your File object.

<pre class="lang:java decode:true">File directory = new File("/some/directory/");
directory.listFiles(directoryFileFilter);</pre>

Its pretty straight-forward.

You could easily produce a function that takes a directory path (as a string) and make it return a list of folders inside that directory.

<pre class="lang:java decode:true ">public List&lt;String&gt; findFoldersInDirectory(String directoryPath) {
    File directory = new File(directoryPath);
	
    FileFilter directoryFileFilter = new FileFilter() {
        public boolean accept(File file) {
            return file.isDirectory();
        }
    };
		
    File[] directoryListAsFile = directory.listFiles(directoryFileFilter);
    List&lt;String&gt; foldersInDirectory = new ArrayList&lt;String&gt;(directoryListAsFile.length);
    for (File directoryAsFile : directoryListAsFile) {
        foldersInDirectory.add(directoryAsFile.getName());
    }

    return foldersInDirectory;
}</pre>

&nbsp;

Credit to: <http://www.avajava.com/tutorials/lessons/how-do-i-use-a-filefilter-to-display-only-the-directories-within-a-directory.html>