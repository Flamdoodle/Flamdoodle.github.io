---
layout: post
title:  "Transforming a Blog With Jekyll"
---

You like the title?  Get it?  I assure you it's better than the other titles I had in mind.  Anyway, if you don't know what Jekyll is or you're not sure how to get started with it, keep on reading.  This post is designed to help you start a blog using Jekyll (not transform one, sorry about the misleading title).

<h3>What is Jekyll?</h3>

Jekyll is a Ruby gem that creates static websites quickly and with little effort.  These sites start out as blogs, but can be turned into whatever you want.  Jekyll is awesome, so let's stop talking about it and start using it.

<h3>Jekyll New</h3>

Getting Jekyll up and running in easy.  Impossibly easy.  But don't run and Hyde from it thinking that something is wrong.  Instead, go to the terminal and type in `gem install jekyll`.  Step 1: check.

Phew, that was easy, right?  Maybe now there's something difficult?  Nope.  Type in `jekyll new your-blog`, hit enter, and watch as Jekyll adds a folder to the current directory with your blog inside.

What do I mean?  Well, `cd` into `your-blog` and type in `jekyll serve`.  This will start a server on your localhost in port 4000.  Go to that in your browser and see the beginnings of your beautiful new blog.

*You may notice that the styling looks a lot like mine.  This is Jekyll's default css.  I happen to like it, but I'll change it in the future.  First order of business is to teach you things, then I'll make it pretty.*

Woah!  Look at everything that Jekyll gave you.  The blog has a title.  Links to Twitter, GitHub, email, and about page.  It even has a post.  But wait, none of that is yours.  This is your blog, so let's make it your own.

<h3>From Jekyll to Doodle, Transformation Complete!</h3>

We have some default Jekyll information in places that we'd rather have our own, so let's change that.  The first place we should look is in the root of our blog, at the `_config.yml` file.  Here is where much of the magic happens that will make this site your own.  What do you want your title to be?  Bam, change it right there.  What email address do you want on the site (if any)?  How about the description of your blog?  It's all right there for you to alter and add to as you want.  Try it out!  If you want to see your changes update in real-time, use `jekyll serve --watch`, this will rebuild your blog every time you save (which is totally awesome and time saving).

Now that most of your personalization is complete, let's move on to the important stuff: your posts and content.  Jekyll makes this really easy too.  Check out the `_posts` folder.  You should read that initial post; it gives you lots of important information quickly, and shows you Jekyll conventions.  The quick version: Jekyll post file names should be in YYYY-MM-DD-name-of-post.ext format, where ext is the file type of your choice (I use markdown).  You also have access to awesome syntax highlighting for writing code snippets.

Besides that, you can change the CSS in the `css` folder, change the layouts in the `_layouts` folder, and make an awesome about page in the `about.md` file.  You can see some of the changes I made to the initial Jekyll skeleton on my [Jekyll repo][jekyll-repo]. Now you have all you need to tell the world about what you think.

<h3>Showing the World Your Words, With GitHub Pages</h3>

You can see your blog on your localhost, but how do you get others to see your beautiful words?  Since you're looking at this and trying to use Jekyll, you probably also have a GitHub account.  What you may not know is that having that account also gives you your own website of sorts.  The url of this site is `username.github.io`.  Create a repo with the name `username.github.io`, `git init` your Jekyll folder, `git add remote` to that repo, and push to master.  If you wait a few minutes...boom!  You have a blog on your own site!  It's that easy.

If you want to learn more about Jekyll, head over to the [main site][jekyll].  You can also checkout out more information about [GitHub Pages][github-pages].  If you want comments at the bottom of the page like I have, checkout [Disqus][disqus].  You can just copy and paste the code they give you into your layout.

[jekyll-repo]: https://github.com/Flamdoodle/Flamdoodle.github.io
[jekyll]: http://jekyllrb.com/
[github-pages]: https://pages.github.com/
[disqus]: https://disqus.com/websites/