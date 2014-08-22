---
layout: post
title:  "Don't 'Bash' Your Head Against a Wall"
---

**Second draft, one month later, still can't get enough of these profiles**

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

*Before I go any further, I'll let you in on a secret.  To help you all out and give others the ability to comment on it, I've put my **[bash profile][profile]** on GitHub.*

There are many, many, MANY more customizations you can make, and some awesome sites that help you understand what's going on.  A quick internet search will also give you many other blog posts like this one.

And you've reached the end (except for some more of my favorite things below).  I hope this helps some people come out of there `shell`s and make their lives easier.  Even more than that, however, I would like people to talk about what they'd like to have and to share their interesting functions or entire profiles (which will lead to a possible project in the future). :D

So, I've decided that my bash profile has gotten too confusing on GitHub and I want to show people some of my favorite parts of it on here.  So below, you'll see some parts of my profile that I have found to be super helpful or nice looking.  *Note: I'm not an expert at bash and some of what I'll put here works and I ahve no idea why.  Sometimes it works only sometimes.  Maybe you can come up with something better.**


{% highlight bash %}
# Push to current branch
function publish() {
  gbranch="`git branch &>/dev/null`"
  git push origin $gbranch
}
{% endhighlight %}

{% highlight bash %}
# Some aliases for database commands in development
alias booms='be rake db:drop; be rake db:create && be rake db:migrate && rails s'
alias seeds='be rake db:drop; be rake db:create && be rake db:migrate && rake db:seed && rails s'
{% endhighlight %}

{% highlight bash %}
# Start a rails server with command 's' and view in Chrome.
function s() {
  osascript -e 'tell application "Terminal" to activate' -e 'tell application "System Events" to tell process "Terminal" to keystroke "t" using command down' -e 'tell application "Terminal" to do script "openchromehost" in selected tab of the front window'
  rails server
}
# For use in function s()
function openchromehost() {
  sleep 3 && open -a "Google Chrome" "http://localhost:3000"
}
{% endhighlight %}
Woah, what's going on up there?  I just added this the other day.  It starts up a rails server, opens a new Terminal tab to work in (because the first one is now running a server), and goes to localhost:3000 in Chrome.  Why didn't I just use the `sleep` function after calling `rails server`?  Well, because the server is running and while it's doing that, no other commands will run, so something clever needed to be done.  Can you figure out how I got it to work?  Look into `osascript`...

{% highlight bash %}
# Clones a repo, CDs into it, opens it in Sublime, and runs bundle. From: https://github.com/stephenplusplus/dots/blob/master/.bash_profile
function clone {
  local url=$1;
  local repo=$2;

  if [[ ${url:0:4} == 'http' || ${url:0:3} == 'git' ]]
  then
    # just clone this thing.
    repo=$(echo $url | awk -F/ '{print $NF}' | sed -e 's/.git$//');
  elif [[ -z $repo ]]
  then
    # my own stuff.
    repo=$url;
    url="git@github.com:flamdoodle/$repo";
  else
    # not my own, but I know whose it is.
    url="git@github.com:$url/$repo.git";
  fi

  git clone $url $repo && cd $repo && subl . && bundle install;
}
{% endhighlight %}
This one is one of my favorites.  See what it does in the commented out bit.  Once you use it, you'll never stop.

{% highlight bash %}
# Opens bash profile
alias bp='subl ~/.bash_profile'
{% endhighlight %}
Easy access!

{% highlight bash %}
# Shows name (in cyan), current working directory (in green), current branch (in pink)
PS1='\[\e[1;96m\]\u: \[\e[0;32m\]\W \[\033[00m\]$(git branch &>/dev/null; if [ $? -eq 0 ]; then echo "\[\e[0;35m\][$(git branch | grep ^*|sed s/\*\ //)] \[\033[00m\]"; fi)>> '
{% endhighlight %}
This the part of your Terminal before your cursor look like:<br>
<img src="/images/terminal-stuff.png"><br>
Doesn't that look awesome?

{% highlight bash %}
# Some aliases that make my life so much easier
alias code='cd ~/Documents/Projects'
alias smart='cd ~/Documents/Projects/smartipants && subl .'
alias whats='cd ~/Documents/Projects/whats-this-2.0 && subl .'
alias bashp='cd ~/Documents/Projects/bash_profile && subl bash_profile'
alias blog='cd ~/Documents/Projects/flamdoodle-blog && subl .'
alias doc='cd ~/Documents'
alias reload='source ~/.bash_profile' # Reloads bash profile without closing Terminal
alias f='open -a Finder ./'
{% endhighlight %}
These are my most frequented projects/most used commands, and these aliases make like so much easier.

[NOTES: Also .gitconfig file.  Other personalization?  More talk on functions, looks like JS?]:blank
[alias]:http://alias.sh/
[profile]:https://github.com/Flamdoodle/bash-profile