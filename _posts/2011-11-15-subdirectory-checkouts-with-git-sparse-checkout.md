---
title: Subdirectory Checkouts with git sparse-checkout
date: 2011-11-15 17:17:20 -05:00
tags:
- git
- read-tree
- sparse-checkout
- svn
meta:
permalink: "/2011/11/15/subdirectory-checkouts-with-git-sparse-checkout/"
---
<p>If there is one thing I miss about SVN having switched to git (and trust me, it’s the only thing), it is the ability to checkout only a sub-tree of a repository. As of version 1.7, you can check out just a sub-tree in git as well! Now not only does git support checking out sub-directories, it does it better than subversion!</p>
<h2>New Repository</h2>
<p>There is a bit of a catch-22 when doing a sub-tree checkout for a new repository. In order to only checkout a sub-tree, you’ll need to have the <kbd>core.sparsecheckout</kbd> option set to <kbd>true</kbd>. Of course, you need to have a git repository before you can enable sparse-checkout. So, rather than doing a <kbd>git clone</kbd>, you’ll need to start with <kbd>git init</kbd>.</p>
<ol>
<li>
<p>Create and initialize your new repository:</p>
<pre class="shell">mkdir  &amp;&amp; cd 
git init
git remote add –f  </pre>
</li>
<li>
<p>Enable sparse-checkout:</p>
<pre class="shell">git config core.sparsecheckout true</pre>
</li>
<li>
<p>Configure sparse-checkout by listing your desired sub-trees in <kbd>.git/info/sparse-checkout</kbd>: </p>
<pre class="shell">echo some/dir/ &gt;&gt; .git/info/sparse-checkout
echo another/sub/tree &gt;&gt; .git/info/sparse-checkout</pre>
</li>
<li>
<p>Checkout from the remote:</p>
<pre class="shell">git pull  </pre>
</li>
</ol>
<h2>Existing Repository</h2>
<p>If you already have a repository, simply enable and configure sparse-checkout as above and do <kbd>git read-tree</kbd>.</p>
<ol>
<li>
<p>Enable sparse-checkout:</p>
<pre class="shell">git config core.sparsecheckout true</pre>
</li>
<li>
<p>Configure sparse-checkout by listing your desired sub-trees in <kbd>.git/info/sparse-checkout</kbd>: </p>
<pre class="shell">echo some/dir/ &gt;&gt; .git/info/sparse-checkout
echo another/sub/tree &gt;&gt; .git/info/sparse-checkout</pre>
</li>
<li>
<p>Update your working tree:</p>
<pre class="shell">git read-tree -mu HEAD</pre>
</li>
</ol>
<h2>Modifying sparse-checkout sub-trees</h2>
<p>If you later decide to change which directories you would like checked out, simply edit the sparse-checkout file and run <kbd>git read-tree</kbd> again as above.</p>
<p>Be sure to read the <a href="http://schacon.github.com/git/git-read-tree.html#_sparse_checkout">documentation on read-tree/sparse-checkout</a>. The sparse-tree file accepts file patterns similar to .gitignore. It also accepts negations—enabling you to specify certain directories or files to <strong>not</strong> checkout.</p>
<p>Now there isn’t <em>anything</em> that svn does better than git!</p>
