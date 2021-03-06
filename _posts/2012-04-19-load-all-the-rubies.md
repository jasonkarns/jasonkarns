---
title: LOAD ALL THE RUBIES!!!
date: 2012-04-19 16:57:25 -04:00
tags:
- cucumber
- ruby
meta:
permalink: "/2012/04/19/load-all-the-rubies/"
---
<h2>Dangerous Cucumber Loading Issue</h2>
<p>I recently discovered a <a href="https://github.com/cucumber/cucumber/issues/269">potentially dangerous issue with how cucumber loads ruby files</a>. The standard cucumber project expects a <kbd>features</kbd> directory in which to place your <kbd>.feature</kbd> files. Standard practice is to place supporting ruby files in <kbd>features/support</kbd> and to place step definitions in <kbd>features/step_definitions</kbd>, but that's just convention. Cucumber recursively loads <em>all</em> .rb files under <kbd>features/</kbd> (ensuring only that <kbd>features/support/env.rb</kbd> is loaded first). This is all well and good, so long as you actually have a features directory (and it's in the root of your project). So what happens if you name your features directory something else or your features directory is in a sub-directory? If you remember to tell cucumber which directory to load from, everything is fine (<kbd>`cucumber alternative_folder/`</kbd>). If you forget, however, cucumber will dutifully load (recursively) <strong>every ruby file it can find</strong>!</p>
<h3>format_hard_drive.rb</h3>
<p>This is still not much of a problem, assuming all your ruby files are just plain old ruby classes or benign ruby scripts. The problem really rears it's head if, say, you have a <kbd>utility_scripts</kbd> directory full of potentially dangerous scripts for setting up project directories, manipulating test databases, or pretty much anything. (Who else has an <code>`rm -rf /`</code> ruby script?)</p>
<p><img class="alignnone size-full wp-image-473" src="{{ site.baseurl }}/assets/2012/04/3ouy3w1.jpg" alt="Cucumber - Load All The Things!!!" width="320" height="240" /></p>
<h3>Lesson</h3>
<p>Name your features directory <kbd>features</kbd>.</p>
