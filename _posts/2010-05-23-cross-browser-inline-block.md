---
title: Cross Browser Inline-Block
date: 2010-05-23 22:53:18 -04:00
tags:
- css
- inline-block
- layout
meta:
permalink: "/2010/05/23/cross-browser-inline-block/"
---
<p>How many times have you used <code>float:left</code> to make a bunch of elements align horizontally? Usually this technique is used on lists (of both the <code>ul</code> and <code>ol</code> persuasion) and generally works just fine under a few preconditions. The first precondition is that you are comfortable using some form of a clear-fix hack. Either you apply <code>overflow:hidden</code> to the container, or you add a meaningless empty div with <code>clear:both</code>, or you apply some magic with the <code>:after</code> pseudo-class. While this isn’t a deal breaker, it is annoying.</p>
<p>The second precondition is that all floated elements are of the same (fixed) height. Of course, your original mock-ups with dummy data and <em>lorem ipsum</em> text all use the same element just repeated across the page, right? And then the client provides actual content (hopefully), and you find that some items have a really long title, or a super-tall product image. And what happens? The floats 'snag' items and you end up with this:</p>
<p><img class="alignnone size-full wp-image-497 aligncenter" src="{{ site.baseurl }}/assets/2010/05/float_thumb-2.png" alt="float_thumb" width="465" height="335" /></p>
<p><a href="http://jsfiddle.net/4pvyg/7/">see fiddle</a></p>
<p>If the previous screenshot is what you going for, or both previous preconditions hold in your case, you may stop reading right now. Otherwise, read on and you’ll learn how to create this instead:</p>
<p><img class="alignnone size-full wp-image-488 aligncenter" src="{{ site.baseurl }}/assets/2010/05/final_thumb.png" alt="final_thumb" width="465" height="273" /></p>
<p><a href="http://jsfiddle.net/4pvyg/16/">see fiddle</a></p>
<p>First, I must give credit where credit is due. The technique I’m about to describe (and improve upon) was <a href="http://blog.mozilla.com/webdev/2009/02/20/cross-browser-inline-block/">covered by Ryan Doherty</a> over at the Mozilla WebDev blog. I suggest you read his post first because I’m going to breeze through his foundation and jump into my improvements.</p>
<h3>Foundation</h3>
<p>Here is the HTML will be working with:</p>
<pre><code>
&lt;ul&gt;
  &lt;li&gt;
    &lt;h3&gt;Product 1&lt;/h3&gt;
    Some product description.
  &lt;/li&gt;
  &lt;li&gt;
    &lt;h3&gt;Product 2&lt;/h3&gt;
    Some product description.
  &lt;/li&gt;
  &lt;li&gt;
    &lt;h3&gt;Product 3&lt;/h3&gt;
    Some really, super, long product description.
  &lt;/li&gt;
&lt;/ul&gt;
</code></pre>
<p>And some aesthetic styles not relevant to the inline-block layout:</p>
<pre><code>
ul {
  list-style:none;
  width:440px;
}
li {
  border:1px solid #888;
  -moz-border-radius:3px;
  width:75px;
  text-align:center;
  margin:5px;
}
h3 {
  font-size:14px;
  font-weight:bold;
  margin:.25em;
}
p {
  margin:.25em;
}
</code></pre>
<h3>Compliant Browsers</h3>
<p>The first step is to try an use the proper CSS property: <code>display:inline-block</code>. This property gives an inline element, block-like properties. Such as the ability to have <code>width</code> and <code>margin</code>. With just this property, <a href="http://www.quirksmode.org/css/display.html">we have support</a> in Firefox 3+, Safari 3+, Chrome 1+, Opera 9+, and IE8+. Not too shabby.</p>
<pre class="css"><code>li {
    display:inline-block;
}</code></pre>
<p><img class="alignnone size-full wp-image-502 aligncenter" src="{{ site.baseurl }}/assets/2010/05/valign_thumb.png" alt="valign_thumb" width="481" height="273" /></p>
<h3>Fixing the Rest: Firefox 2</h3>
<p>Aside from IE 6 and 7, only Firefox 2 fails to support inline-block. To get support in Firefox 2, simply add the mozilla-specific property <code>display:-moz-inline-stack</code> prior to the <code>display:inline-block</code> declaration. Non-Gecko browsers will ignore the -moz rule. Firefox 3+ supports inline-block so it will override the -moz-inline-stack rule. Using the -moz-inline-stack rule for Firefox 2 also necessitates a <code>div</code> be wrapped around the inline-block element’s contents. Given Firefox 2’s latest market share numbers (most give it under 1% overall), I would generally concede that messing with -moz-inline-stack and an inner-wrapping <code>div</code> is unnecessary. For this reason, I have removed the -moz-inline-stack rule from my Inline-Block gist on GitHub, however, you can <a href="http://jsfiddle.net/4pvyg/15/">see it in action</a> at jsfiddle. Feel free to add it back in yourself if Firefox 2 support is necessary.</p>
<h3>Fixing the Rest: IE 6/7</h3>
<p>IE 6 and 7 both support inline-block natively but with a caveat; they only support it on elements that are inherently inline. Thus, block elements like <code>div</code> and list-item elements like <code>li</code> won’t apply inline-block. However, IE 6/7 has the concept of ‘layout’. (see <a href="http://www.satzansatz.de/cssd/onhavinglayout.html">On Having Layout</a>). IE treats elements with layout triggered exactly the way inline-block elements are supposed to work; that is, block-level elements that are displayed inline. So for IE6/7 we reset the display to inline, and trigger hasLayout with <code>zoom:1</code>.</p>
<p>* Note: You can apply the IE 6/7 rules in any manner you wish. Conditional Comments paired with IE-only stylesheets is generally the preferred method. However, I have gone with the *hack in this case to make these utility classes copy/paste-able.</p>
<pre class="css">li {
    display:inline-block;
    *zoom:1;
    *display:inline;
}</pre>
<p>The final touch is to set <code>vertical-align:top</code> to make the boxes line up across the top:</p>
<pre class="css">li {
    display:inline-block;
    *zoom:1;
    *display:inline;
    vertical-align:top;
}</pre>
<p><img class="alignnone size-full wp-image-504 aligncenter" src="{{ site.baseurl }}/assets/2010/05/final_thumb_3.png" alt="final_thumb_3" width="465" height="273" /></p>
<h3>Room for Improvement</h3>
<p>So now we have our elements aligned horizontally without using floats. We have one last problem which is where I will improve on Ryan’s method. In the screenshot below I have changed the <code>li</code> margin to <code>margin:5px 0;</code> We would expect the left and right borders of each box to touch, no?</p>
<p><img class="alignnone size-full wp-image-505 aligncenter" src="{{ site.baseurl }}/assets/2010/05/whitespace_thumb.png" alt="whitespace_thumb" width="441" height="273" /></p>
<p>The problem is due to the fact that white-space surrounding inline elements is displayed. Of course, this makes perfect sense. Imagine if the white-space between words in a sentence weren’t displayed! The trick is to take advantage of <code>letter-spacing</code> and <code>word-spacing</code> to counter the white-space between our inline-block elements. (This is unnecessary in IE6/7 which already ignores the white-space between boxes because the elements have <code>hasLayout</code> triggered and are not technically inline-block.)</p>
<h3>Six of One…</h3>
<p>My first attempt was to apply a negative word-spacing to the container. Word-spacing is inherited, so we must reset it to normal on our inline-block elements themselves so as to not affect their children. With word-spacing set to -1em, we have eliminated the offending white-space in Firefox and Opera.</p>
<p><img class="alignnone size-full wp-image-507 aligncenter" src="{{ site.baseurl }}/assets/2010/05/nowhitespace_thumb.png" alt="nowhitespace_thumb" width="425" height="273" /></p>
<p><a href="http://jsfiddle.net/4pvyg/12/">see fiddle</a></p>
<h3>…Half a Dozen of the Other</h3>
<p>In order to fix WebKit (Safari, Chrome) we must also apply negative letter-spacing. Interestingly, applying <em>only</em> letter-spacing actually fixes both WebKit and Firefox which means that either letter-spacing or word-spacing will work for Firefox. However, in order to appease Opera, we will apply both. <a href="http://jsfiddle.net/4pvyg/13/">see fiddle</a></p>
<h3>All Together Now</h3>
<p>I have pared down the necessary rules to a set of utility classes named ib-container and ib-block, as seen below. You can also find them <a href="http://gist.github.com/247649">in a gist</a> on GitHub and <a href="http://jsfiddle.net/4pvyg/16/">as a fiddle</a> on jsFiddle.</p>
<pre class="css">.ib-block {
    vertical-align:top;
    display:inline-block;
    *zoom:1; /* IE6/7 */
    *display:inline; /* IE6/7 */
}
.ib-container {
    letter-spacing:-.25em;
    word-spacing:-1em;
}
.ib-container .ib-block {
    letter-spacing:normal;
    word-spacing:normal;
}</pre>
<h3>Other Variations</h3>
<p>They can be used on list items as seen in this example or any other set of sibling elements:</p>
<pre><code>
&lt;div class="ib-container"&gt;
    &lt;div class="ib-block"&gt;…&lt;/div&gt;
    &lt;div class="ib-block"&gt;…&lt;/div&gt;
    &lt;div class="ib-block"&gt;…&lt;/div&gt;
&lt;/div&gt;
</code></pre>
<p>They can be used without the ib-container class if the white-space between ib-block elements is not an issue for you:</p>
<pre><code>
&lt;ul&gt;
  &lt;li class="ib-block"&gt;…&lt;/li&gt;
  &lt;li class="ib-block"&gt;…&lt;/li&gt;
  &lt;li class="ib-block"&gt;…&lt;/li&gt;
&lt;/ul&gt;
</code></pre>
<p>They can be nested so an ib-block element becomes an ib-container for other ib-block elements:</p>
<pre><code>
&lt;ul class="ib-container"&gt;
  &lt;li class="ib-block ib-container"&gt;
    &lt;div class="ib-block"&gt;…&lt;/div&gt;
    &lt;div class="ib-block"&gt;…&lt;/div&gt;
  &lt;/li&gt;
  &lt;li class="ib-block ib-container"&gt;
    &lt;div class="ib-block"&gt;…&lt;/div&gt;
    &lt;div class="ib-block"&gt;…&lt;/div&gt;
  &lt;/li&gt;
  &lt;li class="ib-block"&gt;…&lt;/li&gt;
&lt;/ul&gt;
</code></pre>
