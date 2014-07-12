---
layout: post
title:  "Got Domain Name? Git In This Post"
---

I'm popular!  Someone looking at my blog was surprised to find that I used [GitHub Pages][github-pages], since the address she saw was for **stephenroth.com**.  She has asked me to write about how I got my domain name to point to this blog, and, considering that it was a fairly alien and difficult process for me, I decided that was a good idea.  In this post, I will outline how I got **stephenroth.com** to point to **flamdoodle.github.io** (thus completely ruining the illusion that this site is anything more than free hosting).

*Disclaimer*:  I'm still not really sure of what I'm doing in some of these steps, and some of them might be wrong or superfluous.  However, I got it to work, and following these steps should help you too.  This is not my forte, but I'll try my best.

<h3>It's Easy, I Swear</h3>

For this post, I'm going to assume that you already have a domain name and you just don't know how to set it up.  I also assume that you are using a blog built with Jeckyll.

The first step is to add a `CNAME` file to your root directory.  Put your domain name in this file, and nothing else, so it just looks like `your-domain-name.com`.

Next, go into the `_config.yml` file and changed the url line to `url: http://your-domain-name.com`. And then you're done!...with Jekyll.

The next set of steps are less intuitive, but fairly simple.  These require you to interact with where you registered your domain name. Do not fear, I will tell you explicitly what to type in to your settings to git them to work.

First, you have to select which domain name you have that you want to redirect to your GitHub page.  Next, you'll have to edit the DNS settings.

Find the `ANAME` records.  These should have something that looks like `@(none)` and `www`, followed by an IP address.  You'll want to change the IP addresses to `192.30.252.153` and `192.30.252.154`.  Make sure to have both `@(none)` and `www` set to `192.30.252.153` and `192.30.252.154`.  This will mean 4 total records, two for each IP address.
*Note*:  You may see something that looks like `*.example.com` on the same page.  GitHub tells you not to mess with this record as it can screw things up.

Finally, go find `CNAME` records.  Find the section that says `ALIAS` and write `your-domain-name.com`.  In the same record, select "Other Host" (or something like that, don't use "www" or other given options) and type in `username.github.io`. *Note*: This step may not be necessary, I did it and am afraid to change it since I have it working now.

And that's it.  Wait a few hours for the internet to learn about the changes you made, and you should have a fancy schmancy blog with your own URL.

If you want to read more about how to set up a custon domain with GitHub Pages, see [this page][pages].

[github-pages]:https://pages.github.com/
[pages]:https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages
