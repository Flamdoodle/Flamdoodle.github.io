---
layout: post
title:  "JavaScript and Turbolinks Are Not BFFs"
---

**But you can change that**

<h3>The Problem</h3>

If any of you are working on projects using Rails 4, you may have noticed your web pages loading much faster than normal.  This is work of Turbolinks, a gem that is included with every `rails new`.  It works by anticipating the other pages within your site that the user could access and preloading them using ajax.  This means that your UX is greatly improved, but has the unintended effect of making your JaveScript wonky.

You may have already run into this and not realized the issue.  A listener may have stopped working or a continuous process keeps running after you've left the page.  On a recent project I worked on (shoutout to [SmartiPants][smartipants]), this is exactly what happened.
*Quick summary*:  [SmartiPants][smartipants] is a game based on a mental performance task that makes you smarter, and is almost completely JavaScript.
When a user pressed the "Play Game" button, a game starts and won't stop for about 45 seconds (when it finishes).  This all works fine, but the issue comes when navigating away from the page while a game is in progress.

When a user navigates to a different page in your site, Turbolinks loads the HTML response that it got from the server in the background.  What it **doesn't** do is reload your JavaScript.  In the case of [SmartiPants][smartipants], this meant the game would continue to run if you navigated away from the page while it was still going.  The game would continue to play itself without you, and if you came back to the original page, it would pretty much look like your game was haunted.

<h3>The Fix</h3>

When I was working on this problem in [SmartiPants][smartipants], I felt like everything I understood about JavaScript was wrong.  Why wasn't the JavaScript on the next page loading? Why was the original JavaScript continuing on other pages?

It turns out that this is basically what was happening, and Turbolinks was to blame.  It was loading HTML when I asked for it, but wasn't reloading the JavaScript because it was just using the HTML response from the server.

There are several fixes to this issue, and I'll lay out some of the ones I like here.

The first is to change the way you tell your JS to wait for the document to be ready.  Originally, you'll probably have something that looks like:
{% highlight javascript %}
$(document).ready(){
  // your code here
}
{% endhighlight %}
However, this will not work with Turbolinks since your document is only ready once, and any other page that "loads" is in fact only replacing the old HTML on the page.

To fix this, instead write:
{% highlight javascript %}
var ready;
ready = function(){
  // your code here
};
$(document).ready(ready);
$(document).on('page:load', ready)
{% endhighlight %}
While more verbose, this will tell your JS to perform your ready function every time you load a new page, even through Turbolinks, and you'll still get the super load speeds that Turbolinks provides.

Don't like this idea?  Maybe your still having issues?  Maybe you don't like Turbolinks, or don't want it on this specific page?  No problem!  Just make the body tag of your page (or layout) look like this:

{% highlight html %}
<body data-no-turbolink>
  <!-- your code here -->
</body>
{% endhighlight %}

Now you don't have to worry about Turbolinks anymore!  You could also, of course, just remove the gem from your project, but sometimes you just want to deal with a problem later, and this allows that.

And there you have it, Turbolinks and JavaScript can be buddies, but you have to help them out a bit.  If you want to get more information on Turbolinks, checkout out this [RailsCast][railscast], the [Turbolinks repo on GitHub][turbolinks], and, as usual, use your favorite search engine for everything else.

[smartipants]: smartipantsgame.com
[railscast]: http://railscasts.com/episodes/390-turbolinks
[turbolinks]: https://github.com/rails/turbolinks