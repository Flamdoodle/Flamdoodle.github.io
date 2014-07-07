---
layout: post
title:  "JavaScript and Turbolinks Are Not BFFs, But You Can Change That"
---

If any of you are working on projects using Rails 4, you may have noticed your webpages loading much faster than normal.  This is work of Turbolinks, a gem that is included with every `rails new`.  It works by anticipating the other pages within your site that the user could access and preloading them using ajax.  This means that your UX is greatly improved, but has the unintented effect of making your JaveScript wonky.

You may have already run into this and not realized the issue.  A listener may have stopped working or a continuous process keeps running after you've left the page.  On a recent project I worked on (shoutout to [SmartiPants][smartipants]), this is exactly what happened.
  Quick summary:  SmartiPants is a game based on a mental performance task that makes you smarter, and is almost completely JavaScript.
When a user pressed the "Play Game" button, a game starts and won't stop for about 45 seconds (when it finishes).  This all works fine, but the issue comes when navigating away from the page while a game is in progress.

[smartipants]: smartipantsgame.com