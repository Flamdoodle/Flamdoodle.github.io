---
layout: post
title:  "Setting Up SimpleCov, Simply"
---

I was recently told about the test coverage gem [SimpleCov][simplecov].  I immediately fell in love (though maybe it's because it told me I had nearly 100% coverage).  Here, I'll detail the very...simple...setup of SimpleCov in your project and talk quickly about how to use it.
<h3>The Setup</h3>

Adding SimpleCov to your project, as the name suggests, is simple. All that you need to get it up and running is three lines of code.

First, add it to your Gemfile in the test group:

{% highlight ruby %}
gem 'simplecov', :require => false, :group => :test
{% endhighlight %}

This ensures that it is used when you run your tests and that it's not required in the rest of your project, since it's mostly unnecessary.

Next, require it in your test_helper file (this is your spec_helper if you use RSpec).  Copy and paste this into the top of the file:

{% highlight ruby %}
require 'simplecov'
SimpleCov.start 'rails'
{% endhighlight %}

SimpleCov automatically creates a coverage file in your root directory, so add this to your .gitignore for good measure.

Don't forget to `bundle`!
<h3>Using SimpleCov</h3>

Using SimpleCov is as easy to use in your project as it was to install.  The setup we just did makes it so that running your tests also runs SimpleCov.

When you run your tests, SimpleCov should print out a percentage of your test coverage and a file path to the location that the coverage report was saved to.  Copy and paste that location into your browser to get more specific details on your coverage.  If you click on index.html on the page that pops up, you will be directed to a page that looks like the root directory of your project.  Search around!  This is where I decided I loved SimpleCov, since I could see the specific test coverage of each line of my program.

Now go have fun with this tool, and see if you can reach that 100% that we all aspire to.

To see more in-depth documentation, see [SimpleCov][simplecov] on GitHub.

[simplecov]: https://github.com/colszowka/simplecov
