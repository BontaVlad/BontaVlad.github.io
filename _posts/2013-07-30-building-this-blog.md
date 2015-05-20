---
layout: post
title: Building This Blog
tags: blogging
---

This is the third iteration of my blog. This is a meta post on how it was constructed and why certain choices were made.

## Powered By

Prior to this, I tried to adopt the following blogging apparatus:

   * [Wordpress.com](http://wordpress.com/): You can still see my [old blog](http://halfclosed.wordpress.com/). I hated the web editor. I had to often use raw HTML while composing posts to get certain styles right (eg. I wanted my images with a black border, sometimes floated left, etc.). Code formatting was also an issue with the limited set of languages supported. Further, a free Wordpress.com blog disallows editing the CSS.
   * [nanoc](http://nanoc.stoneship.org): My nanoc blog still [exists](http://emaadmanzoor.github.io/eyeshalfclosed/blog/) along with its [code](https://github.com/emaadmanzoor/eyeshalfclosed). nanoc is a very well-documented, extremely powerful static site generator. I struggled with its power for a while and resented needing access to an entire Linux development environment just to publish a post.

Jekyll strikes the middle ground. Jekyll sites can be built automatically by Github pages, so I can use the Github UI (Zen Mode FTW!) or [prose.io](http://prose.io) to compose and commit posts. I no longer require access to a
development machine; I can even do this on my phone!

Jekyll is also extremely simple, and as a consequence, a lot more limited in ability than nanoc. This is magnified if you restrict yourself to automatic publishing via Github pages, where custom plugins are disallowed. I preferred
this trade-off so I could remain minimal, both in my blog's appearance and in the code that powers it.

Another big plus for Jekyll is the sheer number of people using it to host blogs. These users communicate and contribute a lot more actively than nanoc's, presumably due to the Jekyll code-base's tiny learning curve. This is why you see projects like [Octopress](http://octopress.org) and [Jekyll Bootstrap](http://jekyllbootstrap.com) springing up, and a huge number of themes and plugins. When I started with nanoc, there was a single [nanoc-starter](https://github.com/mgutz/nanoc3_blog) project that is still unmaintained; I had no giant shoulders to stand on.

## Design

The theme this blog wears is hand-crafted; I found it way easier than adapting someone else's theme, thought I did search a lot for something minimal in code and appearance that was also responsive.

Some of the themes I considered before rolling my own are:

   * [Minimal Mistakes](http://mademistakes.com/articles/minimal-mistakes-jekyll-theme.html): This is a beautiful theme by Michael Rose, but the code presented too great a learning curve.
   * [So Simple](http://mademistakes.com/articles/so-simple-jekyll-theme.html): Another beautiful theme by Michael Rose, with the same problem as above.
   * [Greyshade](http://shashankmehta.in/archive/2012/greyshade.html): A Medium-esque Octopress theme.
   * [Left](http://zachholman.com/posts/left/): A clean, white Jekyll theme.

The design has some key influencers:

   * [The PureCSS Blog Layout](http://purecss.io/layouts/blog/): PureCSS also forms the backbone of this blog.
   * [Medium.com](http://medium.com): Particularly their layout for an individual post.
   * [Aaron Moodie's Blog](http://aaronmoodie.com/): Follows a Tumble-log style, with different post types.
   * [mnmlist](http://mnmlist.com/): An inspiration for life too.
   
I also use icons from [FontAwesome](http://fortawesome.github.io/Font-Awesome/icons/), which I first stumbled upon on Zach Holman's [Left](http://zachholman.com/posts/left/) Jekyll theme.
