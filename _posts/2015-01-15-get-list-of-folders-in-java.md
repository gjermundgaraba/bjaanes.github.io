---
id: 75
title: Get list of folders in Java
date: 2015-01-15T18:27:47+00:00
author: Gjermund Bjaanes
layout: post
guid: http://maximumdeveloper.com/?p=75
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

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_6">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fget-list-of-folders-in-java%2F&linkname=Get%20list%20of%20folders%20in%20Java" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fget-list-of-folders-in-java%2F&linkname=Get%20list%20of%20folders%20in%20Java" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Fget-list-of-folders-in-java%2F&linkname=Get%20list%20of%20folders%20in%20Java" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>