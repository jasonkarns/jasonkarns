---
title: Google Analytics Tagging with HTML5 data-* Attributes
date: 2010-03-10 00:55:45 -05:00
tags:
- google-analytics
- html5
- javascript
- jquery
- mootools
meta:
  original_post_id: '359'
  _wp_old_slug: '359'
permalink: "/2010/03/10/google-analytics-tagging/"
---
<p>Imagine if you will, a page with a significant amount of dynamic page elements. For instance, a slide-out panel containing a number of ‘panes’ containing topical information on various ‘factors’. Let’s assume that once this slide-out is open, we wish the user to be able to jump from factor to factor (similar to a slideshow) using buttons along the bottom of each factor. Let’s go even deeper and say that within each factor, we have a collection of close-up images. Again, the user should be able to navigate the close-ups via next/previous buttons similar to a slideshow. In addition to the next/previous buttons, along the top edge of the ‘close-ups’ section are progress indicator dots that highlight according to which close-up is active (and link directly to individual close-ups).  Given that this functionality should work without JavaScript, all of these UI controls are marked up as links. And we have quite a few of them—to wit, <var>x*(x-1)</var> factor links (for <var>x</var> factors) plus <var>x*y</var> (direct links to close ups per factor) plus <var>x*(2y)</var> (next/prev links for each <var>y</var> close-up for each factor). So, let’s say we have 3 factors and 3 close-ups per factor. We now have 33 links! And now the task is to tag each of these links with unique labels that will be sent back to Google Analytics upon each click event. I’ve broken down a brief subset of the analytics tags for each of the three types of links below.</p>
<h3>Tag Templates</h3>
<p>Tagging template for the factor navigation along the bottom of each [x] factor:</p>
<pre>/page_name/factor_[x]/factor_1_icon
/page_name/factor_[x]/factor_2_icon
/page_name/factor_[x]/factor_3_icon</pre>
<p>Tagging template for the prev/next buttons on each [y] close-up on each [x] factor:</p>
<pre>/page_name/factor_[x]/closeup_[y]/next_arrow
/page_name/factor_[x]/closeup_[y]/prev_arrow</pre>
<p>Tagging template for the close-up direct links (also used as progress indicator) on each each [x] factor:</p>
<pre>/page_name/factor_[x]/closeup_dot_1
/page_name/factor_[x]/closeup_dot_2
/page_name/factor_[x]/closeup_dot_3</pre>
<h3>Approach</h3>
<p>As with anything, I try to keep my code DRY. Considering that these tags will likely end up as magic strings in some form or another, I’d like to reduce the maintenance overhead of these tags as new factors or close-ups are added or removed. The tags themselves convey the hierarchy of the structure in which they are contained. So let’s map the tagging hierarchy onto the structural hierarchy. This tagging information could be embedded in the <code>id</code> or <code>class</code> attributes of an element, though I think that would be coupling two separate needs (JS behavior/CSS styling + Analytics) onto the same data. This information could also conceivably go into the <code>title</code> attribute, though this attribute is meant for human (read: end-user) consumption. Nothing seems to fit, so let’s try out an <a href="http://dev.w3.org/html5/spec/dom.html#embedding-custom-non-visible-data">HTML5 data-* attribute</a>: <code>data-ga</code>.</p>
<p>First, the /page_name segment should map to the page:</p>
<pre><code>&lt;body data-ga="/page_name"&gt;
</code></pre>
<p>Each ‘factor_[x]’ segment should map to its own factor pane:</p>
<pre><code>&lt;ul class="factors"&gt;
  &lt;li data-ga="/factor_1" /&gt;
  &lt;li data-ga="/factor_2" /&gt;
  &lt;li data-ga="/factor_3" /&gt;
&lt;/ul&gt;</code></pre>
<p>Each ‘closeup_[y]’ segment should mapt to its own close-up pane:</p>
<pre><code>&lt;ul class="closeups"&gt;
  &lt;li data-ga="/closeup_1" /&gt;
  &lt;li data-ga="/closeup_2" /&gt;
  &lt;li data-ga="/closeup_3" /&gt;
&lt;/ul&gt;</code></pre>
<p> </p>
<p>And each link or button gets its own respective value. Keep in mind, multiple <code>data-ga</code> values will be ‘scoped’ by their ancestors’ <code>data-ga</code> values:</p>
<pre><code>&lt;a href="#factor-1" data-ga="/factor_1_icon" /&gt;
&lt;a href="#factor-1-closeup-1" data-ga="/closeup_dot_1" /&gt;
&lt;a href="#factor-1-closeup-2" data-ga="/next_arrow" /&gt;
&lt;a href="#factor-1-closeup-3" data-ga="/prev_arrow" /&gt;
</code></pre>
<p>Now, whenever a link is clicked, we simply concatenate the data-ga values from each ancestor! The method below should have the context of <code>this</code> as an anchor element with a <code>data-ga</code> attribute. Generally, it would be in the click handler of any element matching the selector: <code>"a[data-ga]"</code>. Once <code>ga</code> is concatenated, it can be used as the tag for a Google Analytics API call (<code>_trackPageview</code> or <code>_trackEvent</code>).</p>
<pre class="javascript">$("a[data-ga]").click(function(event){
  var ga = $(this).parents('[data-ga]').andSelf()
           .map(function(){return $(this).attr('data-ga');});
  ga = $.makeArray(ga).join('');
  _pageTracker._trackPageview(ga);
});</pre>
<h3>Demo</h3>
<p><a href="//jsfiddle.net/eY4cq/1/embed/">//jsfiddle.net/eY4cq/1/embed/</a></p>
<h3>A few additional notes</h3>
<h4>Performance</h4>
<p>It would be much better to calculate the ga-tag for every link on the page during page load and cache the result in the data store of the element. As written, the ancestor traversal is executed on every click, and would result in the same return value each time. However, as a special case when I was first implementing this, there were some widgets that altered the hierarchy of the page, thus it was necessary to only perform the concatenation at event-time rather than load-time.</p>
<p>As an additional performance boost, I added a class of <code>ga-scope</code> to each ancestor element that contained a <code>data-ga</code> attribute. This allowed me to use a class selector in the <code>.parents()</code> filter. This will only yield a performance boost in browsers that support a native implementation for querying by class name, thus allowing the selector engine (MooTools or jQuery) to avoid stopping to inspect every single ancestor on its way up the tree.</p>
<h4>MooTools</h4>
<p>I originally implemented this with MooTools. During the implementation I discovered a <a href="https://mootools.lighthouseapp.com/projects/2706-mootools/tickets/649">bug</a> in the MooTools selector parser where the attribute selector doesn’t properly find attributes with hyphens. So, I created a custom pseudo-selector as a workaround:</p>
<pre class="javascript"><code>Selectors.Pseudo.data_ga = function(){
  return Boolean($(this).get('data-ga'));
};</code></pre>
<pre class="javascript"><code>$$('a:data_ga').addEvent('click', function(event){
  var ga_code = this.getParents('.ga-scope')
                .get('data-ga').reverse().join('')
                + this.get('data-ga');
});</code></pre>
