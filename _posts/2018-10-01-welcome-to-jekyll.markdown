---
layout: post
title:  "Using Jekyll with GitHub Pages"
date:   2018-10-01 19:45:46 -0500
permalink: /blog/:title
---

1. You would want to download Ruby. On a Windows system, you would be using the Ruby installer. Make sure to add it to the PATH so that you can use it through your command line.

2. Run the below command within the directory that you want to create your website in.
{% highlight ruby %}
gem install jekyll bundler
{% endhighlight %}

3. And then you create a new Jekyll site using
{% highlight ruby %}
jekyll new myblog
{% endhighlight %}
Where you should replace myblog with the name of your directory

OR

Fork an existing Jekyll repository. But, depending on the directory, you may have to run the below command again
{% highlight ruby %}
gem install jekyll bundler
{% endhighlight %}

4. Now the fun part. You get to build it and run in on a local server. Probably http://localhost:4000

{% highlight ruby %}
bundle exec jekyll serve
{% endhighlight %}

This is used instead of "jekyll serve" if you have a gemfile.

This is all outlined in the [Jekyll documents](https://jekyllrb.com/docs/). However, to deploy it github pages, you would need to head to your Gemfile and comment out the jekyll version line, while uncommenting the github-pages line.

Commit and push your file to [username].github.io and you should be done! Your brand new website should be on https://[username].github.io

There is a series on YouTube by Mike Dane called Jekyll - Static Site Generator that I'm planning to go through.