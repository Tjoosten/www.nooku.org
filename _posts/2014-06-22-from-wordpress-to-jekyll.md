---
title: From Wordpress to Jekyll
author: Nick
layout: post
permalink: /blog/2013/03/from-wordpress-to-jekyll/
---

Did you notice? Probably not. Last month we switched off the database responsible for keeping our blog up and running and moved to a static solution using [Jekyll][1].

<img src="https://farm6.staticflickr.com/5114/14294033867_cd87468a66_z.jpg" alt="jekyll" width="100%" />

For those not familiar, Jekyll is an awesome open source generator of static sites written in Ruby. Jekyll can generate HTML pages from [Markdown][5] and other markup syntax, without the
need for a database.

<!--more-->

Don’t get us wrong. Wordpress is great for blogging, if you are looking for a simple and streamlined user interface that requires almost no technical knowledge. If you have a group of uber trained geeks running around, well, Wordpress is a bit overkill.

Jekyll to the rescue! Jekyll not only makes things simpler, leaner and faster, because the blog is now a static site it also provides a few additional benefits:

* We don't need to run php and mysql where we host the blog, resulting in less resources used on our servers, near to zero maintenance and increased security.
* We now have an improved publishing flow for the team using [Git][6], and one less login account for each of us to remember.

## How to switch from Wordpress to Jekyll.
While switching from Wordpress to Jekyll we had learned a few things along the way that might be useful if you are considered a similar transition.

### 1. Properly export and convert every Wordpress post to Markdown syntax.
For this, we used the [Wordpress to Jekyll exporter][2]: a one-click Wordpress plugin that converts all posts, pages, taxonomies, metadata and settings to Markdown for you, ready to be dropped into Jekyll.

### 2. Create an archive navigation similar to what is built-in into Wordpress.
Luckily Jekyll allow for plugins to be added in order to solve such needs, and a plugin that does just that is the [jekyll-monthly-archive-plugin][3].

### 3. Adding readmore separator to post lists. 
When exporting wordpress posts using the Jekyll exporter, the Wordpress read more markup is exported as well into the new markdown files, in the form of:
{% highlight html %} <!--more--> {% endhighlight %}
  
By taking advantage of [Liquid][4] (the template engine that come with jekyll, which supports HTML as well as various flavours of markdown) you can simply use the liquid split filter by writing something like this:
{% highlight html %}{% raw %}{{ post.content | split:"<!--more-->" | first }}{% endraw %}{% endhighlight %}

### 4. Disquss threads. 
We have some nice discussions going on here on the blog and we didn't want to lose them. Thankfully the Jekyll exporter also add the “dsq_thread_id”  to the generated markdown files. You can just access them via Liquid where you call the Disqus js plugin:
{% highlight html %}{% raw %}
var disqus_identifier = '{{ page.dsq_thread_id }}'; 
var disqus_url = 'http://blog.nooku.org{{ page.permalink }}'; 
{% endraw %}{% endhighlight %}
( the same with the url and permalink)


We are pretty happy with our Jekyll, if you are interested to learn what Jekyll can do for you? Head over [jekyllrb.com][1] to learn more.

Happy coding!



 [1]: http://jekyllrb.com/
 [2]: https://github.com/benbalter/wordpress-to-jekyll-exporter
 [3]: https://github.com/shigeya/jekyll-monthly-archive-plugin
 [4]: http://docs.shopify.com/themes/liquid-basics
 [5]: http://en.wikipedia.org/wiki/Markdown
 [6]: http://git-scm.com/