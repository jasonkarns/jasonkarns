---
title: Announcing jQuery.Firebug
date: 2009-01-06 14:49:29 -05:00
tags: debugging firebug javascript jquery
permalink: "/2009/01/06/announcing-jqueryfirebug/"
---

I have been sitting on my latest [jQuery](http://jquery.com/) plugin for some time now.
Although I realize that the code is not yet of production quality
and there are certainly bugs and features that remain to be addressed,
I've decided that I should at least release this plugin to the wild.
At the very least, I would love some feedback on it and possibly new features to be added.
"So let's see it!" you ask?

jQuery.Firebug is a jQuery plugin that simply exposes the
[Firebug Console API](http://getfirebug.com/console.html) to the jQuery object.
That's about it.
Under the covers, it bridges some functionality between [Firebug](http://getfirebug.com/)
and [Firebug Lite](http://getfirebug.com/lite.html) and has a host of other small feature.
But all in all, it simply adds the Console API methods directly to the jQuery object.

The goal of this plugin is to allow inspection of your jQuery selections while in the middle of a chain.
For those of you who have ever had a jQuery chain like:

~~~js
$(".elements").parents("div")
.find(".new").show().end()
.find(".old").hide();
~~~

and you load up the page and it doesn't work.
How do you begin debugging?
You open up Firebug but are unable to easily 'step through' the jQuery chain.
Inevitably, you have to break up each selector,
assign it to a temporary variable solely to call console.log(temp) on your selection.
Enter jQuery.Firebug:

~~~js
$(".elements").log()
.parents("div").log()
.find(".new").log()
.show().end().log()
.find(".old").log()
.hide();
~~~

Each log method returns the same selection that was passed to it,
so you can simply continue your chain as if it weren't even there.
Every Firebug method (as of Firebug 1.2) is supported so you can call
`debug()`, `assert()`, `info()`, `dir()`, `profile()`, etc.

There are a few additional features that I will address later as the code begins to settle down.
For now, the source and documentation can be found in Subversion at
[svn.jasonkarns.com/jquery/firebug](http://svn.jasonkarns.com/jquery/firebug/).
There is much work to be done on the plugin as well as on the documentation.
Until then, let me hear any feedback you may have.
