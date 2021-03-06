---
title: JavaScript Best Practices
date: 2010-02-25 21:49:47 -05:00
tags:
- javascript
meta:
  original_post_id: '359'
  _wp_old_slug: '359'
permalink: "/2010/02/25/javascript-best-practices/"
---
<p>@<a href="https://twitter.com/ikeif">ikeif</a> recently <a href="https://twitter.com/ikeif/status/9637495634">tweeted</a> a request for some JavaScript best practices. Rather than simply reply to him, I thought I’d post them here and beat him to the blog-post-punch. I’m not going to expand much on any of these, although any discussion that arises will likely spawn its own post. These are in no particular order and are really nothing more than a brain-dump. I’ve numbered them for easy reference in the comments.</p>
<ol>
<li>Avoid global variables. When you must use a ‘global’, use your own namespace.</li>
<li>Avoid cluttering the global namespace with functions. Assign your ‘global’ functions to a single namespace (see above).</li>
<li>Discover the JavaScript framework/library that speaks to you and stick with it. Don’t load jQuery and Prototype on the same project. Yes, I know you can run many libraries in noConflict mode now, but think of the additional overhead you are placing on your users. All for some snazzy plugin? Port it!</li>
<li>Use <a href="http://www.jslint.com/">JSLint</a>. I assume you validate your HTML? Use JSLint to validate your JavaScript. If your code is JSLint safe, you can avoid a few browser idiosyncrasies (hasOwnProperty() anyone?). As a bonus, JS-Lint safe code is also <a href="http://javascript.crockford.com/jsmin.html">JSMin</a> safe so you can minify your scripts without worrying if the minification will affect functionality.</li>
<li>A side effect of using the JSLint validator in <a href="http://www.aptana.com/">Aptana</a>, my IDE of choice for front-end development, is my use of JSLint’s special `/*global */` comment. JSLint will flag any global variables unless they are explicitly listed as dependencies in this comment. This means at the top of all of my scripts, one can easily spot any required dependencies (specific MooTools modules for instance).</li>
<li>Use feature detection not browser sniffing.</li>
<li>Write unobtrusive scripts instead of inline event handlers.</li>
<li>Keep your styles in your CSS! Although most libraries make it easy to manipulate element styles, it’s much better to keep your styling where it belongs- in your CSS. Mixing the two violates separation of concerns and makes your code less maintainable. Instead, add and remove classes as necessary in your scripts.</li>
<li>Make sure your UI elements support proper interaction when JS is disabled. If a link opens a lightbox, set the href to point to the lightbox content so no-JS users can still access the content. Links with `href=”#”` kill kittens.</li>
<li>Any UI elements that *only* support JavaScript interaction (and think carefully about this) should be created by JavaScript. Don’t litter your HTML will dummy elements that are only there for JS events. Your script should create and inject them.</li>
<li>If at all possible, don’t modify libraries or plugins directly. This makes future upgrades a nightmare. It is much better to extend the plugin/library without modifying the original.</li>
<li>Your .js files should be served with HTTP `Content-Type: application/javascript`. BUT the `type` attribute in your HTML `script` element must be `text/javascript` or else Internet Explorer will crap itself.</li>
<li>Language=”JavaScript” was deprecated, like, a zillion years ago. Stop using it.</li>
<li>Don’t pre-optimize your code by using fancy looping structures. It is much better to have readable code. Once your app is running, then you can go back and profile it to eliminate bottlenecks. There is no point in pre-optimizing your scripts when the overhead of your background image is 10x slower.</li>
<li>Don’t return false from an event listener when all you really want is event.preventDefault(). Maybe someone else wants to listen for that click event, too, mmmkay?</li>
<li>Stop using document.write</li>
</ol>
<p>Okay, that’s my list. I may add more later. Disagree with any of these? What best practices or anti-patterns do you have?</p>
