---
id: 126
title: Roommates (Story of my first real App)
date: 2015-02-07T12:40:01+00:00
author: Gjermund Bjaanes
layout: post
guid: http://maximumdeveloper.com/?p=126
permalink: /roommates-story-of-my-first-real-app/
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
  - 3493920148
suevafree_template:
  - right-sidebar
categories:
  - Uncategorized
tags:
  - Mobile
  - Programming
---
I have just launched my new app on App Store and Play Store. It’s an app for organizing shared housing. Living with Roommates made easy &#8211; basically.

&nbsp;

# The story

The idea for this app came to life during the last year of computer engineering school. We either had to come up with a final project for the degree ourselves, or be handed some teacher-made stuffy project. I knew right away that I needed to come up with an idea for myself, because I really wanted to mould a large project from start to finish.

I wanted to make an mobile app. Because its fun to do mobile. I wanted to make software made for users &#8211; I like that much better than stuff nobody really interfaces with. I also wanted to do sync, cloud, users &#8211; there were many things I wanted to do with this app &#8211; just to learn it (I love learning new things!). And cross-platform. I need to think cross-platform. In this case that meant iOS and Android.

I had lived with many different kinds of people on many different occasions and knew what a pain it could be and the struggles with keeping things organized. So I though that might be a cool problem to solve &#8211; with an app. So thats what I did. Or I should say we. Because while the idea originated from me, the project group developed it from basic idea to a functional product as a team.

After the project was finished, we all graduated with fine scores and all was well. I did however feel a bit sad that our awesome project was going to die. So I got back into the code and started to clean it up. Both the iOS and the Android app had some bugs and minor design issues, so I went right away and cleaned those up.

After 6 months or so doing some after-hours work on the polishing of the app, I only had the hardest part left; getting the thing up on the stores (arguably, I now think getting people to notice the app is a much harder problem to solve). I should really say Store (SINGULAR). Because Play Store was a breeze compared to App Store. All the certificates and this and that, all of it has to be in all the right places for everything to be OK. But, I did it, and now it is available on both.

App Store: <a href="https://itunes.apple.com/us/app/roommates-shared-housing-made/id959844470?ls=1&mt=8" target="_blank">Roommates for iOS</a>

Play Store: <a href="https://play.google.com/store/apps/details?id=com.gjermundbjaanes.apps.roommates" target="_blank">Roommates for Android</a>

&nbsp;

# How the app is built

Roommates has four main areas (or screens. or scenes) to keep things organized within your household. Its Feed, Me, Tasks and Expenses.

&nbsp;

[<img class=" wp-image-127 alignleft" src="http://maximumdeveloper.com/wp-content/uploads/2015/02/4.7feed.png" alt="4.7feed" width="300" height="534" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7feed.png 750w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7feed-169x300.png 169w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7feed-576x1024.png 576w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7feed-600x1067.png 600w" sizes="(max-width: 300px) 100vw, 300px" />](http://maximumdeveloper.com/wp-content/uploads/2015/02/4.7feed.png)[<img class=" wp-image-128 alignleft" src="http://maximumdeveloper.com/wp-content/uploads/2015/02/4.7me.png" alt="4.7me" width="300" height="534" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7me.png 750w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7me-169x300.png 169w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7me-576x1024.png 576w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7me-600x1067.png 600w" sizes="(max-width: 300px) 100vw, 300px" />](http://maximumdeveloper.com/wp-content/uploads/2015/02/4.7me.png)[<img class=" wp-image-129 alignleft" src="http://maximumdeveloper.com/wp-content/uploads/2015/02/4.7tasks.png" alt="4.7tasks" width="300" height="534" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7tasks.png 750w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7tasks-169x300.png 169w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7tasks-576x1024.png 576w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7tasks-600x1067.png 600w" sizes="(max-width: 300px) 100vw, 300px" />](http://maximumdeveloper.com/wp-content/uploads/2015/02/4.7tasks.png)[<img class=" wp-image-130 alignnone" src="http://maximumdeveloper.com/wp-content/uploads/2015/02/4.7expenses.png" alt="4.7expenses" width="300" height="534" srcset="http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7expenses.png 750w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7expenses-169x300.png 169w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7expenses-576x1024.png 576w, http://gjermundbjaanes.com/wp-content/uploads/2015/02/4.7expenses-600x1067.png 600w" sizes="(max-width: 300px) 100vw, 300px" />](http://maximumdeveloper.com/wp-content/uploads/2015/02/4.7expenses.png)

**Feed** is household notes (think of Post It’s on the fridge or a physical bulletin-board) and household events.

**Me** is the user and household management section.

**Tasks** are for task lists (todo&#8217;s and such).

**Expenses** is for splitting up expenses between roommates.

&nbsp;

This app is built with an BaaS (Backend as a Service) product called Parse. It allows all the data to live in the cloud, managed entirely by them. They provide an SDK with an easy-to-use API that is fast to get started with. It made the syncing and data management part extremely easy. All that was left to do was design the architecture, app and data. And code the clients. So lots of work really, but it was nice to not manage our own backend all the way.

Parse provides a feature called Cloud Code. It&#8217;s Javascript code that lives in the cloud that can be called from the clients. It also provides some hooks for specific events (like delete and create for different classes). Not everything is implemented in Cloud Code, but the most critical logic lives nicely up there in this cloud.

The app is made for iOS and Android, and each application is built with the native tools, instead of using some cross-platform SDK. Both apps have the same feature set and work together (both sync with the same data from Parse).

&nbsp;

I am very happy to have made this release happen, and I hope someone will find it useful. All the code is also available on Github:

Roommates for iOS: <a href="https://github.com/bjaanes/Roommates-For-iOS" target="_blank">https://github.com/bjaanes/Roommates-For-iOS</a>
  
Roommates for Android: <a href="https://github.com/bjaanes/Roommates-For-Android" target="_blank">https://github.com/bjaanes/Roommates-For-Android</a>
  
Roommates Cloud Code: <a href="https://github.com/bjaanes/Roommates-For-CloudCode" target="_blank">https://github.com/bjaanes/Roommates-For-CloudCode</a>

&nbsp;

I have also made a simple landing page for Roommate:

<a href="http://maximumdeveloper.com/roommates" target="_blank">http://maximumdeveloper.com/roommates</a>

&nbsp;

&nbsp;

&nbsp;

<div class="addtoany_share_save_container addtoany_content_bottom">
  <div class="a2a_kit a2a_kit_size_32 addtoany_list a2a_target" id="wpa2a_12">
    <a class="a2a_button_facebook" href="http://www.addtoany.com/add_to/facebook?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Froommates-story-of-my-first-real-app%2F&linkname=Roommates%20%28Story%20of%20my%20first%20real%20App%29" title="Facebook" rel="nofollow" target="_blank"></a><a class="a2a_button_twitter" href="http://www.addtoany.com/add_to/twitter?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Froommates-story-of-my-first-real-app%2F&linkname=Roommates%20%28Story%20of%20my%20first%20real%20App%29" title="Twitter" rel="nofollow" target="_blank"></a><a class="a2a_button_google_plus" href="http://www.addtoany.com/add_to/google_plus?linkurl=http%3A%2F%2Fgjermundbjaanes.com%2Froommates-story-of-my-first-real-app%2F&linkname=Roommates%20%28Story%20of%20my%20first%20real%20App%29" title="Google+" rel="nofollow" target="_blank"></a><a class="a2a_dd addtoany_share_save" href="https://www.addtoany.com/share"></a>
  </div>
</div>