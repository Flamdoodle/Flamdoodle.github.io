---
layout: post
title:  "Don't 'Bash' Your Head Against a Wall"
---

**First draft, sorry if it's scattered, some people wanted this information ASAP**

So, I'll admit that I have a bit more of a `shell`fish reason for this post.  I want this post to educate people, but also start a discussion that I can benefit from.  I finally got around to customizing my bash profile the other day.  For months I've been putting it off, always telling myself that there were better things to work on than figuring that mess out.  WHY DIDN'T SOMEBODY TELL ME HOW WRONG I WAS?!

So here's the deal, there are super simple ways of customizing your bash profile, and not so simple ways.  All this pretty much comes down to learning the syntax.  As a novice, I'm a fan of the simple things, but they are also the ones that are most time-saving for me.

`alias` == the best thing ever

Don't believe me?  Well, do you get tired of typing in `git status`?  What about `git checkout`?  `git push origin`?  Then make an alias!  Just type in `gs`, or `gc`, or `gpo`.  You won't realize how much you really hated doing all the typing until you don't have to do it anymore.

If you don't know how to access your bash profile, just type in the following into your terminal `subl ~/.bash_profile`.  Of course, this assumes you are using Sublime Text as your editor of choice (as it is for me).  It also assumes that you already have access to the `subl` command...which, if you don't, you can add to in your bash profile :D!

In any case, `subl ~/.bash_profile` (or a similar command) will open up the bash profile in your text editor.  Here, you'll probably see some pre-existing code, added by various other programs and as default.  Don't touch these unless you know what you're doing.  However, you can add to it to your heart's content.

Start out with something simple.  For me, this was typing in `alias ga='git add'`.  If you save the profile and restart your current bash session, you can now use `ga` instead of `git add`, and it works exactly the same!  Wooooaahhhhh.  This was the point when I realized that I had been missing out on something powerful.

`alias` is just the tip of the iceberg.  Learn the other predefined functions...or create your own!  One of my favorite (that I've taken from [this cool site][alias]) `cd`s me into the directory of just created:
{% highlight bash %}
function mcd() {
  mkdir -p "$1" && cd "$1";
}
{% endhighlight %}
And that's it.  But it's convenience cannot be ignored.  Usually when I create a new directory, I want to be working within it immediately after creation.  This makes that happen.  So simple, yet so satisfying.

There are other, more complex functions that you can create, like the one that opens the GitHub page for the directory I'm currently working in.

*Before I go any further, I'll let you in on a secret.  To help you all out and give others the ability to comment, I've uploaded my [bash profile][profile] to GitHub.*

There are many, many, MANY more customizations you can make, and some awesome sites that help you understand what's going on.  A quick internet search will also give you many other blog posts like this one.

And you've reached the end (of draft #1).  I hope this helps some people come out of there `shell`s and make their lives easier.  Even more than that, however, I would like people to share their interesting functions or entire profiles (which will lead to a possible project in the future). :D




[NOTES: I want people to contribute to the conversation to talk about what they've done with their bash or what they would like to do.  Also .gitconfig file.  Other personalization?  More talk on functions, looks like JS?]:blank
[alias]:http://alias.sh/
[profile]:https://github.com/Flamdoodle/bash-profile